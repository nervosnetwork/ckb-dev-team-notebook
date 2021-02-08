# CKB Dev Meeting Mon, Aug 24, 2020

## Agenda

### Details

* **Project**: CKB
* **Time**: 50min, at 1:30pm
* **Meeting Goal**: Plan, Retrospective
* **Meeting Room**: https://meet.google.com/wha-knxv-cwx
* **Host**: ian
* **Attendees**: CKB Dev Team, Jan

### Agenda Items

#### Plan

* **Presenter**: Ian Yang
* **Time Allowed**: 20min
* **Topic**: Progress Update and Weekly Plan

---
## Meeting Notes

---
### Progress Update

@doitian

Last Week:

* [x] Summarize fee bumping and write an essay about it.
* [y] Write an essay about the best practices to manage transaction statuses and utxos.
* [x] Set team OKR

This Week:

* (Cont.) Write an essay about the best practices to manage transaction statuses and utxos.
* Discuss pool requirements with @zhangsoledad and @quake
* Troubleshoot `dao_with_satoshi_cell_occupied`

@quake

Last Week:

* Lightnode UI
    * [g] debug and test
    * [g] run lightnode client on android

This Week:

* Lightnode client demo

* RPC improvement
  * Add hex binary format to chain related rpc
  * Add two merkle proof related rpc
  * Add ping rpc

@zhangsoledad

Last Week:

* [Y] relay tx refactory
* [Y] refactory ResolevdTransaction
* [X] debug benchmark failure 

This week:

* (Cont.) refactory ResolevdTransaction

Comments:

* Freezer: Ready for review
* Wtxid relay: we use txid first 10 bytes as keys in pool and proposals
* Benchmark: switch to new implementation
* Blocking: crossbeam 0.4.3 issue
* Related: Migrate to async arch
* Help @keroro520 on the long fork problem

@driftluo

Last Week:

- [x] Discovery on Go
- [x] According to go implementation, adjust ckb discovery as needed
- [Y] Try to remove ckb `Both` protocol
- [x] Found a stuck problem, and located part of the minimum scene

This week:

- Try to remove ckb `Both` protocol
- Replace example protocol usage of tentacle

Comments:

Prioritize running tentacle in iOS and Browser

@yangby-cryptape

Last Week:

- [g] [Better RocksDB options for HeaderMap](https://github.com/nervosnetwork/ckb/pull/2239).
- [x] [Ensure CKB can run on host with only 800m memory](https://github.com/nervosnetwork/ckb-internal/issues/689)
- [y] Upgrade ckb-bench and the bench bot.
  Reason: spent to much time on memory optimization (above task).
  
This Week:
- [Upgrade ckb-bench and the bench bot.](https://github.com/nervosnetwork/ckb-internal/issues/781)
- [CKB Debug Console](https://github.com/nervosnetwork/ckb-internal/issues/712)
  - Research first.


@keroro520

Last Week:

  * [g] Update tps-bench
  * [g] Extract commonly used behaviors of integration-tests, to improve the programmability and readability
  * [y] Debug issues happened on staging network

This Week:
  * Debug the long forks problem
  * Update `Net` framework of integration-test

@chuijiaolianying

Last Week:

* [y] integration test log monitor #758
* [y] ckb-bench: find best tps bench with different send_delay
* [g] adjust uncle rate in aggron network #789 

This Week:
* ckb-bench: 
    * find best tps bench with different send_delay
    * doc about how to eval tps and how to use new tps bench
* integration test log monitor:
    * check more cases and find how to use log monitor
