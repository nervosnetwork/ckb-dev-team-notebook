# CKB Dev Meeting Mon, Jun 29, 2020

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

Agenda:

* Progress update
* [Q3 Brainstorm](https://nervos.quip.com/zq2nACbtXAdk/CKB-Roadmap-2020-Q3-Brainstorm)

---
## Nervos Briefing

### Dev Tools

[@xxuejie: SUGGEST HERE]

### MAKE

* Live cells index performance tuning

### Research

* Review Adapter Signature
* Study MAD-HTLC and Sprites
* Research confidential transaction on CKB
* Papers and articles:
    * Cryptography
        * Blockchain-based Distributed Attribute based Encryption
        * Incrementally Verifiable Computation via Incremental PCPs
        * On the Size of Pairing-based Non-interactive Arguments [Groth16]
    * Layer X
        * Revive: Rebalancing Off-Blockchain Payment Networks
        * Pisa: Arbitration Outsourcing for State Channels
        * Anonymous Multi-Hop Locks for Blockchain Scalability and Interoperability

### Collaboration

#### § Beihang Crypto Infrastructure

* 完成 R1 等算法的原型
* 新增 RSA 实现需求

---
## Meeting Notes

---
### Progress Update

@doitian

Last Week:
* [x] Windows Memory Tracing
* [x] Review Chain Freezer

This week
* [ ] Refactor RPC error
* [ ] Block structure document

@quake

Last Week
* [ ] Network middleware PoC (blocked)
* [*] Prepare light node wallet demo requirement and rpc doc for MAKE
* [*] Rocksdb memory issue

This Week
* [ ] Channel prototype review https://github.com/Unlocku/Channel-prototype

@zhangsoledad

Last Week
* [ ] freezer continuous improvement
* [*] proposal table issue
* [*] tx-pool review

This Week
* [ ] freezer production-ready
* [ ] fix tx-pool issue

@driftluo

Last Week
- [ ] tentacle-go: the main code is basically completed, and the user layer code and testing are still missing, as well as some language pits that need to be tested

This Week
- complete the final work on tentacle-go
- tentacle has some code that needs to be adjusted

@yangby-cryptape

Last Week

* [x] [Fix integration test spec pack_uncles_into_epoch_starting.](https://github.com/nervosnetwork/ckb-internal/issues/687)
* [Memory Leak Issue](https://github.com/nervosnetwork/ckb-internal/issues/688):
  - [x] Figure out why use so many memories when IBD.
  - [-] Try to find a simple way to trace memory usage of CKB in windows and integrate it into CKB as a feature.
    WPA doesn't work well in my windows 10, so I use DebugDiag 1.2.
  - [-] Try to find a flexible way to replace all `HashMap`, `HashSet` and some other structs, so we can do trace or shrink more easy and more comprehensive.

This Week
- [Research rocksdb WriteBufferManager](https://github.com/nervosnetwork/ckb-internal/issues/689)

@keroro520

Last Week:
  - [x] Review minimum viable freezer
  - [x] Research testground, or maybe other frameworks

This Week:
  - [ ] Prepare a talk about Testground
  - [ ] Write a test plan which simulate tps-bench
  - [ ] Add a test RPC to create a block from pool and connect it to the chain

@chuijiaolianying

Last Week
* [ ] add integration test cases doc
  * [ ] tx_pool
* [ ] read ckb_bench code

This Week
* [ ] continue add integration test cases doc
  * [ ] rpc
  * [ ] consensus
  * [ ] relay

---
### Plan


