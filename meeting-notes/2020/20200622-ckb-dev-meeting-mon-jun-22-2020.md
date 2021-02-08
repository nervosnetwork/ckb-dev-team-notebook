# CKB Dev Meeting Mon, Jun 22, 2020

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

* Keyper hardware wallet integration design
* Neuron live cells refactor
* Keypering implementation
* Refactor Neuron indexer

### Research

* Learn general coin join & GrinJoin specifications
* Read "Flexible Byzantine Fault Tolerance"
* Axon protocol design
* Designing routing schemes for large-scale future channel networks
* Survey on zkSNARKs
* Read "Non-Interactive Zero-Knowledge for NP from Learning with Errors"
* research confidential transaction on CKB

---
## Meeting Notes

---
### Progress Update

@doitian

Last Week

* [x] Review PR
* [x] Release RC versions and patches
* [x] Brainstorm Q3 objectives Reviewed infrastructure layer tasks

This Week

* [ ] Review minimal viable ChainFreezer
* [ ] Improve RPC errors
* [ ] Document block header document
* [ ] Setup CI job to build CKB binary for deployment

@quake

Last Week
* [x] Sync scheduler simulation https://github.com/nervosnetwork/sync-scheduler-simulation-test/pull/5
* [] Network middleware PoC
This Week
* [ ] Network middleware PoC
* [ ] Prepare light node wallet demo requirement and rpc doc for MAKE

@zhangsoledad

Last Week
* [x] minimal viable ChainFreezer

This Week
* [ ] Archive original raw block in ChainFreezer rather than block body
* [ ] Improve ChainFreezer，complement tests and metrics 
* [ ] complement some RPC in passing

@driftluo

Last Week
- [x] Release tentacle alpha 5
- [x] doc about tentacle protocol handle choice
- [x] protocol select impl in go
- [x] review pr

This week
- [ ] tentacle go

@yangby-cryptape

- Last week
  - [x] [Automated Testbed Environment](https://github.com/nervosnetwork/ckb-internal/issues/605)
    TODO: transfer https://github.com/yangby-cryptape/ckb-devops-configs to `nervornetwork`, then push config files to `deploy/staging` branch to deploy staging network automatically.
- This week
  - Fix integration test
  - Fix staging test environment issues

@keroro520

Last Week:

  - [ ] ~~Add docs about Grafana, adding nodes~~
  - [ ] Research testground, or maybe other frameworks
  - [x] Continue net-monitor collect more metrics
  - [x] Write tps-bench documents

This Week:

  - [ ] Review minimum viable freezer
  - [ ] Research testground, or maybe other frameworks

@chuijiaolianying

Last Week

* [ ] read RFCs
* [ ] add integration test cases doc
  * [ ] mining relate cases

This week
* [ ] continue add integration test cases doc

---
### Plan
