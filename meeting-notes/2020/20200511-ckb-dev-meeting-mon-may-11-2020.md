# CKB Dev Meeting Mon, May 11, 2020

---
## Agenda

### Details

* **Project**: CKB
* **Time**: 50min, at 1:30pm
* **Meeting Goal**: Seminar, Brainstorm
* **Meeting Room**: https://meet.google.com/gix-ipdy-efr
* **Host**: ian
* **Attendees**: CKB Dev Team, Jan

### Agenda Items

#### Status Briefing

* **Presenter**: Ian
* **Topic**: Synchronize status
* **Time Allowed**: 20min

#### Test Improvement Discussion

* **Presenter**: Ian
* **Topic**: How to improve our tests
* **Time Allowed**: 30min

https://github.com/nervosnetwork/ckb-internal/issues/579

---
## Meeting Notes

---
### Status Briefing

@doitian

Last week

* Reorganize RPC errors
* Make May Plan
* Write a part of block header document

This week

* Confirm requirements of planned COs
* Refactor send transaction RPC error
* Continue to write the block header document


@quake

Last week

* Light client fork handling
* Code review and bug fix
    * https://github.com/nervosnetwork/ckb/pull/2056
    * https://github.com/nervosnetwork/ckb/pull/2060
    * https://github.com/nervosnetwork/ckb/pull/2063

This week

* Light client fork handling
* BIP157 protocol test

@zhangsoledad

Last Week

* Upgrade RocksDB
* Chain Freezer Design

This Week

* Chain Freezer Design Review
    * Including pruning
    * Coinbase pruning requirement
    * Shared by multiple nodes via netfs
    * CKB has some different design, the cell (utxo) is stored in block.

@driftluo

Last week

- Implementation of a scheduler that dynamically adjusts the timeline

This week

- There are some ideas on the scheduler that need to be tested

@yangby-cryptape

Last week

- Compile CKB in Windows to try to figure out why failed in Windows
    - [A brief summary](ckb-internal/issues/410#issuecomment-626160463)
        - http://nervosnetwork/ckb#2061

  - Review CKB Part of summa-tx/bitcoin-spv and try run it (#380).

- This week

    - #410

    - Update nervosnetwork/ckb#1988 to finished #78, #79 and #367.
  
    - Try #361

@keroro520

Last week

* [Add RPC `truncate`](https://github.com/nervosnetwork/ckb/pull/2064)
* [Fix: return connected address in RPC `get_peers`](https://github.com/nervosnetwork/ckb/pull/2052)
* Add integration tests related connectivity
* Debug [peer reject connection](https://github.com/nervosnetwork/ckb-internal/issues/95) but fail to reproduce.

This week

  * [Bench BlockFetcher get_ancestor](https://github.com/nervosnetwork/ckb-internal/issues/213)
  * https://github.com/nervosnetwork/ckb-internal/issues/119
  * PENDING 3/5 spare

@xxuejie

DT highlights:

* [ckb-simple-account-layer](https://github.com/nervosnetwork/ckb-simple-account-layer), a separate account layer integration for CKB. Works as a Rust crate for now, will provide node.js bindings later
* @jjyr might release a very initial preview version of capsule later this week.

#### Action Items

---
### Test Improvement Discussion

#### Action Items
