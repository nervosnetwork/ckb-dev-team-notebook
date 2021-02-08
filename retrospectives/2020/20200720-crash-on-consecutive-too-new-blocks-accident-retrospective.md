# Crash On Consecutive Too New Blocks Accident Retrospective

* 2020-07-17 @doitian deployed v0.34.0 to testnet.
* 2020-07-18 @doitian received the sentry error: [(VerifierResolver) blocks used for median time exist](http://sentry.nervos.org/share/issue/6dde779db01947fcb70e7dd461b1f737/).
* 2020-07-19 @quake has found out the cause.
* 2020-07-19 @zhangsoledad fixed it in [GHSA-hjqq-29pw-96wj](https://github.com/nervosnetwork/ckb/security/advisories/GHSA-hjqq-29pw-96wj)
* 2020-07-19 @zhangsoledad suggested to add nodes with shifted time in testnet ([#742](https://github.com/nervosnetwork/ckb-internal/issues/742))
* 2020-07-20 @doitian deployed the fixing as v0.33.2 and v0.34.1 to testnet
* 2020-07-22 @doitian released v0.33.2 and v0.34.1

## Cause analysis

> ― Quake Wang, [Jul 18, 2020 at 5:17:11 PM]:
>
> 我找到这个错误的问题了，和之前修复的那个时间太新相关：
> https://github.com/nervosnetwork/ckb/commit/7630eee61cd0766e1974c4a186e37b739946a9b9
> 
> 攻击者可以故意构建一个时间比较新的区块，然后通过 headers 发送过来
> 
> 在修复这个问题之后，在这里：
> https://github.com/nervosnetwork/ckb/blob/7630eee61cd0766e1974c4a186e37b739946a9b9/sync/src/synchronizer/headers_process.rs#L373
> 
> 就直接返回了，没有把它放入到 header_map
> 
> 这样判断 headers 里面的第二个 header ，它去读 parent 就 panic 了
> 
> 测试的话，可以改本机时间到 2019 年 11 月之前，然后跑一个 ckb 从0开始的，这样收到的 headers 里面，第一个就是 too new
> 
> 然后判断第二个的时候就 panic 了

## Related Accidents

* [2020-07-06 Uncle Rate Surge Accident](https://github.com/nervosnetwork/ckb-internal/blob/master/retrospectives/2020/20200706-uncle-rate-surge-accident.md)

## Further Actions

* [#742](https://github.com/nervosnetwork/ckb-internal/issues/742) Testnet 加入一台时间不同步的矿工节点。
* 类似错误之后需要通过模拟对应的环境做长时间的测试。
* 研究使用 P2P 网络时间来调整本地时间在安全性上是否可行
