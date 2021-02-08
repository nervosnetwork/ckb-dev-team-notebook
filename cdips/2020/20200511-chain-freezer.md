# Chain Freezer

## Motivation

解决 archive data 的问题，同时优化 database 的性能。

## Specification

### Geth chain freezer

https://blog.ethereum.org/2019/07/10/geth-v1-9-0/

PR https://github.com/ethereum/go-ethereum/pull/19244


#### Freezer basics
Geth v1.9.0 把数据库拆成两部分：

* 最近的区块和时间状态 仍留在 kv(LevelDB) 里，推荐使用 SSD.
* 3个 epochs (以太坊的 epoch 定义与 ckb 不同， Ethash 定义的每 30_000 块为一个 epoch) 之前的 blocks 和 receipts 从 LevelDB 里移出到 freezer 中，已 append-only flat files 的形式保存，适合使用 HDD.

Geth 可以通过 --datadir.ancient 来指定 freezer 的目录，默认作为 chaindata 的子目录。

从旧版本升级到 v1.9.0，Geth 会运行一次 migration 把数据拆分。

#### Freezer tricks

* 如果 freezer 的数据被删除或不存在， Geth 禁止启动.
* 如果 state 数据被删除或不存在，Geth 会基于 freezer 的数据重建索引和状态并开始同步.

### Bitcoin Core Splitting the data directory

实际上 Geth Freezer 只是复刻了 Bitcoin 目前的存储形式。

https://github.com/bitcoin/bitcoin/blob/master/doc/files.md#data-directory-layout

https://en.bitcoin.it/wiki/Splitting_the_data_directory

Bitcoin Core 默认把所有 data 放到一个 data 目录里.

- 如果你的 data 目录在 HDD 上， 可以通过把 chainstate 目录移到 SSD 来提高性能
- 如果你的 data 目录在 SSD 上， 可以通过把 blk* and rev* 文件移走，节约空间

### CKB freezer

freezer archive 以后的数据可以加载来恢复 state，但是不能进行片断索引。

ckb 移植 freezer 的几种方案：

1. 和 bitcoin 一样创建 statedb 冗余 live cell. ( ckb 目前的实现和bitcoin 是完全不同的 )

    pros: 
    
    - 简洁
    - 优化 resolve transaction.
    - 如果我们考虑后面的 fork 在 header 里加 accumulator, 实现 fast sync 会很简单。
         
    cons: 
    
    - 数据冗余，代价比 bitcoin 高 
    - 会和 *区块并行验证* 的想法有些冲突，区块并行验证是基于 input 检查不依赖 状态来实现的。
       
2. 不改变现有存储，基于之前 prune 的想法，在到达 threshold 保留最新的 live cell.


#### Prune
Prune 的目的其实和 Freezer 接近，都是处理 archive data，不同的是 Freezer 将 archive data 移到冷库，而 Prune 是直接删掉，在实现上是相通的。

## Additional 
### Raw undo data (rev*.dat)

https://bitcoin.stackexchange.com/questions/57978/file-format-rev-dat

和 blk*.dat 对应，记录被对应区块花费掉的UTXOs, 在 DisconnectBlock 的时候会用到。
