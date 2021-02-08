# CKB Dev Meeting Mon, Jul 13, 2020

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

* Research voting via Nervos DAO
* Keypering
* CKB light client MVP
* Ledger and other hardware wallet integration research

### Research

* Research grin’s wallet and contract
* zkSNARK

---
## Meeting Notes

---
### Progress Update

@doitian

Last week

* [x] Q3 Plan
* [x] Add info in transaction verification error

This week

* [ ] Add info in script error
* [ ] Fix Azure integration test

@quake

Last Week:

[] Review channel network protocol 
[] Review Bitcoin and Ethereum RPCs
[] Refactor some storage related traits

This Week:

Continue...

@zhangsoledad

Last week
* [x] chain branch clean
* [x] independent refactory PR
* [ ] redesign transaction resolve, split orphan tx pool

This week
* [ ] fix tx-pool issue https://github.com/nervosnetwork/ckb-internal/issues/692
* [ ] redesign transaction resolve, split orphan tx pool


@driftluo

Last week
- [x] finish test on tentacle-go
- [x] implement asynchronous channels with priority

This week
- replace tentacle priority implementation
- in the process of implementing the channel, I found a problem that I hadn't delved into but instead solved using dirty methods. Requires refactoring code

@yangby-cryptape

Last week
- [ ] [Ensure CKB can run on host with only 800m memory](https://github.com/nervosnetwork/ckb-internal/issues/689)
  - There are 2 PRs used to set rocksdb settings required merge (in discussion with Quake).
  - About header map: 2 PRs require reviews.
 This week
- [ ] [Ensure CKB can run on host with only 800m memory](https://github.com/nervosnetwork/ckb-internal/issues/689)
- [ ] [Logger supports multiple output target, each target can configure different filters.](https://github.com/nervosnetwork/ckb-internal/issues/724)
- [ ] [Embedded metrics service](https://github.com/nervosnetwork/ckb-internal/issues/602)

@keroro520

Last Week

  - [x] Initialize testground-sdk-rust (without integrating influxdb)

This Week

  - [ ] Complete testground-sdk-rust tests // tests tell us what the workflow is and help to complete the sdk-rust implementation
  - [ ] Rewrite testground examples based on sdk-rust
  - [ ] testground rust docker builder

@chuijiaolianying

Last Week:

* [x] [测试 block download scheduler 参数](https://github.com/nervosnetwork/ckb-internal/issues/711)

This Week:

* [ ] 集成测试改进

---
### Plan
