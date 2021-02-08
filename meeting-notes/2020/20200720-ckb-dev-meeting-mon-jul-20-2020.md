# CKB Dev Meeting Mon, Jul 20, 2020

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

### Dev Tools

[@xxuejie: SUGGEST HERE]

### MAKE

* [CKB oracle bridge](https://github.com/duanyytop/ckb-oracle-bridge)
* Keypering
    * [Keypering](https://github.com/liusong1111/keypering)
    * [Keypering Core](https://github.com/liusong1111/keypering-core)
* Ledger nano integration
* Coinbase integration

### Research

* Read Decentralized Custody Scheme with Game-Theoretic Security from Conflux
* Resource-Restricted Cryptography
* zk-Rollups
* The establishment and test of GPC in UDT version.
* Research zether
* Research beam’s wallet

---
## Meeting Notes

---
### Progress Update

@doitian

Last Week

* [x] RPC errors refactoring
* [ ] Fix Windows Integration
* [x] Start research fee mechanism

This Week

* [ ] Fee mechanism research

@quake

Last week

- [*] Review bitcoin and ethereum rpc: https://github.com/nervosnetwork/ckb-internal/issues/729
- [*] Review channel prototype contract https://github.com/Unlocku/Channel-prototype
- [*] Storage trait tweak, waiting for PR: https://github.com/nervosnetwork/ckb/pull/2163

This week

- [ ] Review channel prototype ruby code, add unit test
- [ ] Add more rpc after discussion


@zhangsoledad

Last week
- [*] tx-pool check syntactic correctness before resolve
- [*] re-broadcast when duplicated tx submit
- [ ] tx-pool demand analysis
 
This week
- [ ] coinbase integration
- [ ] continue research tx-pool design

@driftluo

Last week
- [x] remove `set_notify` on tentacle
- [x] review and merge secio refactory(break change)

This week
- Rewrite the tentacle poll
- Rewrite the tentacle buffer

@yangby-cryptape

Last week
- [ ] [Ensure CKB can run on host with only 800m memory](https://github.com/nervosnetwork/ckb-internal/issues/689)
- [ ] [Logger supports multiple output target, each target can configure different filters.](https://github.com/nervosnetwork/ckb-internal/issues/724)
- [ ] [Embedded metrics service](https://github.com/nervosnetwork/ckb-internal/issues/602)

This week
- [ ] Continue previous unfinished tasks.
- [ ] **Block** PRs for Rocksdb are required, to continue PR about `Memory`.
- [ ] **Block** Rust 1.45.0 is required, to continue PR about `Logger` and `metrics`.
  `function-like procedural macros` 的功能会带来对 logger 和 metrics 的较大影响，如果先写代码再升级，可能要 rewrite 很多代码，因此想先升级。
  顺便把旧的一些代码要删掉（目前主库有 2 个 crates 可以 delete）。

@keroro520


Last Week

  - [x] Complete testground-sdk-rust tests // tests tell us what the workflow is and help to complete the sdk-rust implementation
  - [x] Rewrite testground examples based on sdk-rust
  - [x] testground rust docker builder

This Week

  - [ ] Run staging network based on ckb-devops-configs
  - [ ] Debug integration test failure "pool_resurrect"
  - [ ] Continue write ckb-plan based on testground

@chuijiaolianying

Last Week

- [x] 执行更多的同步测试
- [ ] 集成测试优化：
    1. 抽象公共方法；
    2. 添加更具体的注释，帮助理解 case；
    3. 优化 case，包括更有针对性的 verification，拆分 case 等；
    
This Week
 - [ ] 继续集成测试优化

---
### Plan
