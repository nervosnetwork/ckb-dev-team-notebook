# CKB Dev Meeting Mon, Aug 31, 2020

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

* [x] (Cont.) Write an essay about the best practices to manage transaction statuses and utxos.
* [x] Discuss pool requirements with @zhangsoledad and @quake
* [x] Troubleshoot `dao_with_satoshi_cell_occupied`

This Week:

* Survey network fee filter protocols
* Bootstrap documentation KRs
* Do 4 1-1 Meetings

@quake

Last Week:

[g] Lightnode client demo
[y] RPC improvement
  [g] RPC method deprecation
  [g] Add hex binary format to chain related rpc
  [y] Add two merkle proof related rpc
  [r] Add ping rpc

This Week:
* RPC improvement
  * Add two merkle proof related rpc
  * Add ping rpc
  * Add clear_ban rpc
  * Research tx subscription rpc


@zhangsoledad

Last Week:

* [x] crossbeam-channel issue
* [x] staging fork 
* [x] stateless ResolevdTransaction

This Week:

* async/await experiment branch (storage)
* header-first sync abstract

@driftluo

Last Week:

- [y] Try to remove ckb `Both` protocol(need review)
- [x] Replace example protocol usage of tentacle(need review)

This week:

- Add websocket transport on tentacle, just support pc

@yangby-cryptape

Last Week:

- [g] [Upgrade ckb-bench and the bench bot.](https://github.com/nervosnetwork/ckb-internal/issues/781)
- [y] [CKB Debug Console](https://github.com/nervosnetwork/ckb-internal/issues/712)
  - Research first.

This Week:
- [CKB Debug Console](https://github.com/nervosnetwork/ckb-internal/issues/712)
  - A draft PR to show the design and the code structure.
    With features:
    - [Enable/Disable skipping block and transaction verification for developers via Debug Console](https://github.com/nervosnetwork/ckb-internal/issues/710)

@keroro520

Last Week:

  * [g] Update `Net` framework of integration-test
  * [y] Find a better way to construct new block at integration-test
  
This Week:
  * Add `BlockTemplateOptions` and `BlockTemplateParams` to control tx-pool `get_block_template`.
  * Introduce the new version of `rpc::generate_block`, which takes `BlockTemplateOptions` as parameter, to integration tests.
  * Refactor some code style, "tip" is not "parent".

This Week:

@chuijiaolianying

Last Week:

* ckb-tps-bench:
    * [g] find best tps bench with different send_delay
    * [g] add doc for new tps bench
    * [g] move method to eval network stable to configuration
    * [g] add nodes info into tps-bench metrics
* integration test:
    * [r] log monitor

This week:

* ckb-tps-bench
    * generate blocks is there no matured cellbase
    * print bench result
    * find a method find stable bench result
    * work with boyu migrate CI tps-bench

* integration test
    * add thread info in integration log format
    * add more log for util functions

* freezer
   read relate doc and design test cases
