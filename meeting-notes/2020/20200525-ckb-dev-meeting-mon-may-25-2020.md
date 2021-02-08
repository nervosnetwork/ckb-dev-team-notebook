# CKB Dev Meeting Mon, May 25, 2020

## Agenda

### Details

* **Project**: CKB
* **Time**: 50min, at 1:30pm
* **Meeting Goal**: Plan, Retrospective
* **Meeting Room**: https://meet.google.com/gix-ipdy-efr
* **Host**: ian
* **Attendees**: CKB Dev Team, Jan

### Agenda Items

#### Plan

* **Presenter**: Ian Yang
* **Topic**: Progress Update and Weekly Plan
* **Time Allowed**: 30min

---
## Nervos Briefing

### MAKE

* sUDT
* Keypering
* Simplest dApp
* Cells index solutions research and comparison.

[※ source](https://cryptape.quip.com/PmVJAp9VhQwI/MAKE-Weekly)

### Dev Tools

* 3 new members joining DT this week
    + Wanbiao Ye from muta, focus on CKB VM enhancements
    + Peng Hu, new hire, focus on lumos the JavaScript framework development
    + Vlad, new hire, focus on crypto algorithm integration with CKB VM
* Draft tutorial for developing smart contracts on CKB with capsule: https://github.com/nervosnetwork/capsule/wiki/SUDT-tutorial-part-1:-Setup

### Research

* Read "Pisa: Arbitration Outsourcing for State Channels"
* Read "TxChain: Efficient Cryptocurrency Light Clients via Contingent Transaction Aggregation"
* Read Skale, a layer 2 (actually a sidechain protocol) solution on Ethereum.
* Trying to improve Aggelos’ PoS sidechain protocol
* The PCN survey
* zkSNARKs
* Read "Simple Schnorr Multi-Signatures with Applications to Bitcoin"
* Read "Compact Multi-Signatures for Smaller Blockchains"

[※ source](https://cryptape.quip.com/Cda0AP3i1AAr/Research-Weekly)

### Collaboration

#### Beihang Crypto Infrastructure Research

* 优化 SM2 算法，SM2+SM3 链上验签消耗 50M cycles，对比目前的 secp256k1 系统实现为 1.6M，差距为 30 倍
    * 计划进行进一步优化性能，目标为 secp256k1 消耗的 10 倍以内（native 下历史最优大概是 5、6 倍好像）
    * 计划进一步优化 binary 大小，目前 900k
* SM2/SM3 签名算法初步实现完成，需要消耗 0.1B cycles
    * 主要原因是没有应用乘法表等优化方式，后续工作重点改为优化 SM2 算法，预期消耗 cycle 值可以压到 10M 以内
* ed25519 实现完成，cycle 消耗 10M，暂时不进行优化

[※ source](https://cryptape.quip.com/pXkpAs1jCtEf/Beihang-Crypto-Infrastructure-Research-Weekly)

---
## Meeting Notes

---
### Progress Update

┌ @doitian

Last week

* 🚫 Refactor transaction error
    * Not worked on this last week
* 🌨 Organize issues into paths and focus on describing the problems instead of specifying solutions.
    * Partially completed. see #614

This week

* Organize issues in each path
* Refactor transaction error

┌ @quake

Last week

* BIP157 client reference implementation

This week

* BIP157 client reference implementation ( test , debug )

┌ @zhangsoledad

Last week
* cell storage implementation

This week
* test cell storage
* chain freezer implementation

┌ @driftluo

Last week

- The sync optimization series of articles  finished
- the tentacle-go repo completes encryption-related codes, including secp, aead
- Testing the scheduler using normal distribution and Poisson distribution random functions（https://gist.github.com/driftluo/f9d35d9f5da72b938ba8c5fc6ba1aadb）

This week

- Continue to complete tentacle go implementation
- Async blocking article
- p2p long test needs to discuss how to do it

┌ @yangby-cryptape

- Last week

  - [x] [Grants Acceptance Review: bitcoin-spv test](https://github.com/nervosnetwork/ckb-internal/issues/380)
  - [ ] [Automated Testbed Environment](https://github.com/nervosnetwork/ckb-internal/issues/605)
    Just spend few time on it, only do few tests.
  
- This week

  - [ ] [Automated Testbed Environment](https://github.com/nervosnetwork/ckb-internal/issues/605)
    - [ ] Require a simple discussion (ref: [#590](https://github.com/nervosnetwork/ckb-internal/pull/590)).
    - [ ] Split into several operable tasks.
    - [ ] Do tasks.

┌ @keroro520

Last Week:

* [x] [Add failpoints to support Chaos testing](https://github.com/nervosnetwork/ckb-internal/issues/610)

  - [x] Specify the actions of fail-points via the configuration `fail-points` in `ckb.toml`.
  - [x] Add fail-points at the front of sending/receiving network messages.
  - [x] Create `sync/src/utils.rs` to wrap most of the operations of sending messages.
  - [x] Refactor some code.
  - [x] Run 2 nodes from the fresh state, the one configured with `0.1%` probability of network messages lost, another is normal. The former takes `170` minutes and the latter takes `120` minutes to synchronize to the TIP.

This Week:

* [ ] [Setup a long-term staging network. It should support:](https://github.com/nervosnetwork/ckb-internal/issues/621):
    * [ ] Auto deploy when develop branch updates
    * [ ] Transactions generator(tps-bench)
    * [ ] Report tps, system resources usages

* [ ] [Research how to generate and save a Grafana snapshot or a picture of the snapshot. It can be used to report daily metrics.](https://github.com/nervosnetwork/ckb-internal/issues/620)

* [ ] [Collect network latencies with help of `ckb-net-monitor`](https://github.com/nervosnetwork/ckb-internal/issues/43)

### Action Items

* [ ] @doitian Schedule a meeting to discuss the test tasks proposed in #590.
* [ ] Send PR links for tasks due this month.
* [ ] @quake Create a report about whether the DoS issue is in the scope of the code audit but not discovered.
