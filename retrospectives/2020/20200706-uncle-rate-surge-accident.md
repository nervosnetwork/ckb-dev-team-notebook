# Uncle Rate Surge Accident

## Events

开始时间 Jul 1, 2020

* 7/1 @driftluo 观测到测试时本地时间问题会驱逐正常节点发送的 Compact Block 通知。
* 7/1 @driftluo 观测到主网上 Uncle Rate 大幅度上升，导致全网出块间隔升高。
* 7/1 @doitian 创建 Security Advisory [GHSA-r9rv-9mh8-pxf4](https://github.com/nervosnetwork/ckb/security/advisories/GHSA-r9rv-9mh8-pxf4)
* 7/2 @zhangsoledad 修复 GHSA-r9rv-9mh8-pxf4
* 7/3 @doitian 合并 GHSA-r9rv-9mh8-pxf4 并部署到 Testnet 和 Mainnet
* 7/3 @quake 联系矿池和市场，升级到新版本
* 7/6 @TheWaWaR 确认叔块率下降
* 7/6 @driftluo 观测到叔块率又有回升

## Cause

有矿工本地时间没有同步，比真实时间快了15秒以上，导致它一出块就会被其他节点 ban 掉 5 分钟，它就变成了一个孤立的节点。同时它又会持续去连接网络中的其他节点，这样就导致了它会在比较旧的 tip 上工作一段时间，等连接上之后，时间已经过去了，这期间它挖的区块又能被其他节点给接受，这些块就都变成了 uncle block，导致 uncle rate持续居高不下。

## Actions

* @quake 和 @nirenzang 沟通过。目前只有使用全网 3% 的算力，就可以让 Uncle Rate 一直在目标之上，这样难度调整会一直增大难度减少 Epoch blocks 数量来提高出块间隔。从目前的协议设计上很难防止这种攻击，因为假设在没有激励的情况下，是不会有敌手持续发动这种攻击的。
* 是否要忽略时间上过老的区块目前存在分歧。目前是包含的，认为是正常的算力，应该在难度调整中进行统计，缺点是会因为意外导致全网出块间隔被拉长。如果忽略的话需要确定一个阈值，并设计路线图逐步升级网络协议过滤掉通过 CompactBlock 来发送过老的叔块。之后的讨论可以在 [#704](https://github.com/nervosnetwork/ckb-internal/issues/704) 继续。
