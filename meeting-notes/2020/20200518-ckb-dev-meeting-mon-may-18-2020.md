# CKB Dev Meeting Mon, May 18, 2020

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

N/A

### Research

* Jan: Read "UMA Data Verification Mechanism : Adding Economic Guarantees to Blockchain Oracles"
* Alan: Writing polynomial IOP paper. Prepare eurocrypt 2020.
* Cris: Read "From Bilinear Pairings to Multilinear Maps"
* Ke: Read "Bolt: Anonymous Payment Channels for Decentralized Currencies"
* Key: Read "General State Channel Networks"

### Collaboration

#### § Beihang Crypto Infrastructure

* M2/SM3 签名算法初步实现完成，需要消耗 0.1B cycles
    * 主要原因是没有应用乘法表等优化方式，后续工作重点改为优化 SM2 算法，预期消耗 cycle 值可以压到 10M 以内
    * 目标：实用化
* ed25519 实现完成，cycle 消耗 10M，可以进一步优化

---
## Meeting Notes

---
### Progress Update

@doitian

Last Week:

* [x] Confirm requirements of planned COs
* [ ] Refactor send transaction RPC error
    * Added details to the transaction verification error. Finished 2 and a lot to go.
* [ ] Continue to write the block header document
    * Not worked on it last week
* Set up ckb-internal
* A lot of meetings. Sorted the 1-1 feedbacks.

This Week

* Refactor transaction error
* Organize issues into paths and focus on describing the problems instead of specifying solutions.

@quake

* [x] Light client fork handling
* [x] Code review and bug fix
https://github.com/nervosnetwork/ckb/pull/2082
* [x] BIP157 protocol test

This Week:
* [ ] BIP157 client reference implementation

@zhangsoledad

Problems

* P2p blocking flag issue (connect/disconnect/notify)
    * BLOCKING: We need CKB network benchmark to see where to add blocking flags.
    * Bypass the block verification? Ignore consensus limit?

This Week

* Chain Freezer

@driftluo

last week:

- The new version scheduler test is completed in a week, and the average performance is improved by 10% -20%
- Fix the competition between sync and relayer in another way and add an integration test
- Fix block state judgment problem
- The secio-go library has been opened, and aead encryption is currently implemented, which is slowly advancing

This week:

- A blog about synchronization
- Continue to promote Go to achieve

@yangby-cryptape

Last week
  - [x] [#410](https://github.com/nervosnetwork/ckb-internal/410)
    Reviewing.
  - [x] Update [#1988](https://github.com/nervosnetwork/ckb-internal/1988) to finished [#78](https://github.com/nervosnetwork/ckb-internal/78) and [#367](https://github.com/nervosnetwork/ckb-internal/367).
    Reviewing.
  - [ ] [#361](https://github.com/nervosnetwork/ckb-internal/361)
    Problem: could I add a `RwLock` to `RocksDB`?
  - [ ] [#380](https://github.com/nervosnetwork/ckb-internal/issues/380)
This week

* Continue #380 
* Setup tests

@keroro520

Last Week:

* [x] [Bench BlockFetcher get_ancestor](https://github.com/nervosnetwork/ckb-internal/issues/213)
* [x] [Fix last common updation inside BlockFetcher](https://github.com/nervosnetwork/ckb-internal/issues/119)
* [x] [Deploy v0.32.0-rc1](https://github.com/nervosnetwork/ckb-internal/issues/586)

This Week:

* [ ] [Add failpoints to support Chaos testing(https://github.com/nervosnetwork/ckb-internal/issues/610)

---
### Plan

* P2P test
* Staging environment
* Block sync test
