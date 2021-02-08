# CKB Dev Meeting Mon, Aug 10, 2020

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
* **Topic**: Progress Update and Weekly Plan
* **Time Allowed**: 30min

#### Retrospectives

* ckb-test failed on spec block_sync_relayer_collaboration #764
* snappy postmortem
* with-data postmortem

---
## Meeting Notes

---
### Progress Update

@doitian

Last

* [x] Publish the document of bitcoin fee estimation algorithm.
* [x] Research other estimation algorithms.
* [Not started] Research how to improve CKB to support Child-Pay-For-Parent and Replace-By-Fee.

This

* Design fee estimate algorithm for CKB
* Research fee bumping


@quake

Last Week

- [ ] lightnode UI (ongoing)
- [x] Resolve ckb-test failed on spec block_sync_relayer_collaboration
- [x] Snappy security issue

This week
- [ ] lightnode UI 预期还要6～7个工作日完成

@zhangsoledad


Last week
* [x]  tx-pool issue
* [x]  CellProvider issue 
* [ ]  debugging orphan tx 

This week
* [ ] improve cell storage test case 
* [ ] audit code prepare fork


@driftluo

Last week
- [x] Fix secio poll read/write impl
- [x] Rewrite buffer on tentacle(need review)
- [x] Add test on yamux(need review)
- [x] Identify protocol perf(need review)
- [x] Fix yamux mem leak

This week
- Waiting for tentacle release
- Protocol on go

Currently, there are still ping and discovery protocols left unimplemented, and I plan to complete it this week

@yangby-cryptape

Last week
- [x] Review few PRs.
- [x] Fix benchmark errors: blocked when failed to sync in the PR to refactor tx-pool.
- [x] Configure RocksDB in `ckb.toml`.
- [x] Configure Grafana with metrics service.

This week
- Upgrade ckb-bench and the bench bot.
- Refactor app-config so it does not depend on services.
- Metrics for Chain Freezer.
- Better RocksDB options for HeaderMap.

@keroro520

Last Week:

  - [x] Fix the issue that "last_common_header" does not update in time
  - [x] Try more generic traits on ckb_types
  - [x] Debug the issue related "TransactionFailedToVerify: CellbaseImmaturity" during tps-bench

This Week:

  - [ ] Extract commonly used behaviors of integration-tests, to improve the programmability and readability
  - [ ] Refactor some modules of testground-sdk-rust

Q3 Major Tasks:

* Run a staging network, including transactions generator and system monitor. It is like an internal-use testnet network.
* Run several known test scenarios on testground.
* Refactor integration, make it more programable and readable.

@chuijiaolianying

Last Week

* [ ] Create event recorder/monitor based on logfile #758 
* [ ] Add node with time error in Testnet #742 

This Week

* [ ] Finish #758 #742 
* [ ] Prefix integration test log #774 
* [ ] ckb-bench doc #776 

---
### Plan
