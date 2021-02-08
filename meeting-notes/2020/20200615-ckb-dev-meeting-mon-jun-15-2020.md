# CKB Dev Meeting Mon, Jun 15, 2020

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

### MAKE

* Try new languages on CKB VM: Nim, Lua
* Keypering.
* Indexer refactoring such as `lumos-indexer` integration.
* Ledger integration

### Research

* Layer 2
    * Axon protocol
* Payment Channel
    * Designing routings for large-scale future channel networks
    * Investigations on the topology of Lightning and Ripple, trying to model a channel network via Watts graphs
    * Learn from blog.priewienv.me and weekly meetings
* Write survey on zkSNARKs
* Skimmed "How to Delegate Computations Publicly"
* Read "Practical Delegation of Computation Using Multiple Servers"
* Read "You Sank My Battleship! A Case Study to Evaluate State Channels as a Scaling Solution for Cryptocurrencies"
* Read "ForceMove: an n-party state channel protocol"
* Read "Nitro Protocol"
* Read "Pisa: Arbitration Outsourcing for State Channels"

---
## Meeting Notes

---
### Progress Update

@doitian

Last week

* [-] Brainstorm Q3 objectives Reviewed infrastructure layer tasks
* [X] Sort ckb-internal tasks Updated infrastructure layer tasks
* [-] Refactor transaction error Updated several error structs

This week

* [ ] Review PR
* [ ] Release RC versions and patches
* [ ] Brainstorm Q3 objectives Reviewed infrastructure layer tasks

@quake

Last Week
* [X] Headers-first sync difficult verify (uncle)
* Sync scheduler simulation
* Network middleware PoC

This Week
* Sync scheduler simulation
* Network middleware PoC

@zhangsoledad

Last week
* [X] minimum viable freezer

This week
* [ ] reconcile freezer db
* [ ] freezer regression testing

@driftluo

Last week

- [x] ckb security issue
- [x] async blocking [article](https://www.driftluo.com/article/bddaac63-89eb-4ac8-b6f9-7b79a1416faa)
- [x] ckb generate peerid

This week

- doc about tentacle protocol handle choice
- tentacle go

@yangby-cryptape

- Last week
  - [x] feat: change logger filter dynamically via RPC 
  - [ ] [Automated Testbed Environment](https://github.com/nervosnetwork/ckb-internal/issues/605)
    - [x] Ansible playbook programmatically.
  - [x] Review few PRs.
- This week
  - [ ] [Automated Testbed Environment](https://github.com/nervosnetwork/ckb-internal/issues/605)
  - [ ] Finish [CKB PR-1988](https://github.com/nervosnetwork/ckb/pull/1988)

@keroro520

Last Week:

  - [ ] Add docs about Grafana, adding nodes
  - [x] Continue to rewrite tps-bench (expose the bench metrics and system metrics)
  - [ ] Research testground, or maybe other frameworks
  - [ ] net-monitor collect more metrics(85%)


This Week:

  - [ ] Add docs about Grafana, adding nodes, tps-bench
  - [ ] Research testground, or maybe other frameworks
  - [ ] Continue net-monitor collect more metrics

@chuijiaolianying

last week

* [ ] [try testground](https://github.com/nervosnetwork/ckb-internal/issues/636)
* [ ] learn p2p relate in CKB
* [ ] [add ckb integration test doc](https://github.com/nervosnetwork/ckb-internal/issues/107)

this week

* [ ] [try testground](https://github.com/nervosnetwork/ckb-internal/issues/636)
* [ ] [add ckb integration test doc](https://github.com/nervosnetwork/ckb-internal/issues/107)

---
### Plan

