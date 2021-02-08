# CKB Dev Meeting Mon, Jun 1, 2020

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

* Bundle vcredist in Neuron
* Keypering
* Lumos integration research

### Research

* Layer-2 protocols research

### Collaboration

#### § Reputation Research

研究课题基本结束

---
## Meeting Notes

---
### Progress Update

@doitian

┌ @doitian

Last week

* 🚫 Refactor transaction error
    *Not worked on this last week
* [x] Organize issues into paths and focus on describing the problems instead of specifying solutions.

This week

* Brainstorm Q3 objectives
* Sort ckb-internal tasks
* Refactor transaction error

@quake

Last week 

[*] BIP157/158 client reference implementation ( test , debug )

This week

[ ] Headers-first sync difficult verify (uncle)
[ ] ckb as lib 

@zhangsoledad

* Freezer migration
* Freezer: move code data
    * RocksDB transaction does not support `deleteRange`

@driftluo

Last week

- [ ] The `secio-go` handshake process is not implemented
- [x] Fix molecule-go index bug, add some API
- [ ] Async blocking article

This week

- [ ] Continue unfinished work last week
- [ ] Draw a line chart according to the experimental data and adjust the random number sampling in the test

@yangby-cryptape

- Last week
  - [ ] [Automated Testbed Environment](https://github.com/nervosnetwork/ckb-internal/issues/605)
    - [x] Require a simple discussion (ref: [#590](https://github.com/nervosnetwork/ckb-internal/pull/590)).
    - [x] Can start a chain use one command after set few customize parameters (each nodes are same).
- This week
  - [ ] [Automated Testbed Environment](https://github.com/nervosnetwork/ckb-internal/issues/605)
    - [ ] Bring `staging network` back to `ckb init`.
    - [ ] Run Staging Network.
    - [ ] Let staging network can be updated via GitHub push hooks.
        - [ ] Handle GitHub push hooks requests (in a queue).
        - [ ] More customize parameters.

@keroro520

* [ ] TPS Bench

---
### Plan
