# Snappy Postmortem
* 2020-08-02 @quake 在给 lightclient 写测试的时候，对网络消息补了一个 fuzz testing，发现对于某些数据包会 crash
* 2020-08-02 @quake 发现在 CKB 里面用的 snappy 版本写的是 0.2，有个 1.0 的 panic fix，不能通过 bot 自动升级：https://github.com/BurntSushi/rust-snappy/issues/29
* 2020-08-03 @quake 发现在升级之后，fuzz testing 会报 OOM 错误

## Cause analysis

> Quake Wang, [Aug 3, 2020 at 4:59:28 PM (Aug 3, 2020 at 5:07:20 PM)]:
> 我们在处理网络消息的时候，会用 snappy 解压缩：
> https://github.com/nervosnetwork/ckb/blob/687d797f1888dd05d1f38ce6d1bef3e5b9b6e38b/network/src/compress.rs#L68

> 它这里直接 alloc 一个 vec：
> https://github.com/BurntSushi/rust-snappy/blob/master/src/decompress.rs#L106

> 但是 vec len 是通过数据包里面直接读取的，攻击者可以构建一个数据包，让节点 oom（len最大可以设置为 2^32 - 1, alloc 4GB）

> 我写了一个 poc：
> https://gist.github.com/quake/8db935df1d03afb39be5ad1901f09f7f

> 让 @xxuejie 帮忙在他的 1GB 树莓派上跑了一下
> pi@raspberrypi:~ $ ./quake-test
> memory allocation of 4294967295 bytes failedAborted

> 修复方法应该在 decompress 之前，先用 decompress_len 取出来一下，判断如果大于某个值，就直接 ban 对方节点

## Further Actions

* 添加更多的 fuzz testing 
