# CKB Dev Meeting Mon, Aug 3, 2020

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

---
## Meeting Notes

---
### Progress Update

@doitian

Last week:

* Document bitcoin fee estimation algorithm.
    
This week:    

* Publish the document of bitcoin fee estimation algorithm.
* Research other estimation algorithms.
* Research how to improve CKB to support Child-Pay-For-Parent and Replace-By-Fee.

@quake

Last Week 

- [*] Add more RPC
  - move add_node / remove_node rpc to network module
  - add more fields to local_node_info
  - add more fields to get_peers
  
- [] lightnode UI

This Week

- [] lightnode UI

- [] Resolve ckb-test failed on spec block_sync_relayer_collaboration

- [] Snappy security issue

@zhangsoledad

Last week
- [*] transaction resolve with cell storage refactory PR
- [*] reimplement orphan tx process
- [ ] tx-pool issue

This week
- [ ] improve test case
- [ ] prepare fork architecture
- [ ] continue research tx-pool design

@driftluo

Last week
- [x] `sync state` rpc
- [x] Fix potential data race on tentacle go
- [x] Identify protocol on go
- [x] Fix bug on molecule-go and add more tests
- [x] Add control on yamux(need review)
- [x] Fix yamux impl(need review)
- [x] Impl quicksink on priority channel(need review)

This week
- [x] Fix secio poll read/write impl(need review)
- Tentacle can be released
- Impl protocol on go

@yangby-cryptape

Last week
- [x] [Embedded metrics service (PRs)](https://github.com/nervosnetwork/ckb-internal/issues/602)

This week
- [ ] Continue PRs for Rocksdb.
  - [ ] Configure RocksDB in `ckb.toml`.
  - [ ] [Ensure CKB can run on host with only 800m memory](https://github.com/nervosnetwork/ckb-internal/issues/689)
- [ ] Add more metrics (I have few PRs require rebase for new metrics service).

@keroro520

[SUGGEST HERE]

@chuijiaolianying

Last Week

 - [ ]  Use trait refactor integration test
 
This Week

 - [ ] Continue refactor integration test with using trait or other ways
 - [ ] Create event recorder/monitor based on logfile

---
### Plan

PR Review 倡议：

* Reviewer 把 code review 作为第一优先级，如果在 reviewers 列表里，但是没法及时 review 及时反馈
* Reviewee 包装好 PR，提供一份地图方便 reviewers，并更积极推销 PR
* Review 难度大的 PR 看能不能拆分成更小的修改，或者约会议作同步 review
