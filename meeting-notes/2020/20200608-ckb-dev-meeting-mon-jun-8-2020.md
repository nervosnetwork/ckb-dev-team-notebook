# CKB Dev Meeting Mon, Jun 8, 2020

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
## Meeting Notes

---
### Progress Update

@doitian

Last week

* [-] Brainstorm Q3 objectives
    Reviewed infrastructure layer tasks
* [-] Sort ckb-internal tasks
    Updated infrastructure layer tasks
* [-] Refactor transaction error
    Updated several error structs

This week, continue

* Brainstorm Q3 objectives
* Sort ckb-internal tasks
* Refactor transaction error

@quake

Last week
* [ ] Headers-first sync difficult verify (uncle)
* [-] ckb as lib

This week, continue
* Headers-first sync difficult verify (uncle)
* (Maybe) Network middleware PoC

@zhangsoledad

Last week
 * [-]  cell storage 
 * [-]  refactory storage migration
 
This week
 * Continue freezer implementation. Objective: PoC


@driftluo

Last week

 - [x] secio-go finished, it works well
 - [x] secio-rust performance optimization
 - [ ] async blocking article
 
 This week
 
 - ckb security issue
 - https://github.com/nervosnetwork/ckb/issues/2104
 - tentacle go
 - async blocking article

@yangby-cryptape

- Last week
  - [ ] [Automated Testbed Environment](https://github.com/nervosnetwork/ckb-internal/issues/605)
    - [x] Bring `staging network` back to `ckb init`.
    - [x] Configure terraform programmatically.
    - [ ] (blocked) Ansible playbook programmatically.
    - [ ] Let staging network can be updated via GitHub push hooks.
- This week
  - [ ] [Automated Testbed Environment](https://github.com/nervosnetwork/ckb-internal/issues/605)
  - [ ] Claim other tasks during meetings.

@keroro520


Last Week:

  * [ ] Add docs about Grafana, adding nodes

  * [ ] Enhence tps-bench
    - [x] Refactor and fix bugs
    - [ ] Add docs, 2in2out, node version, system arguments
    - [x] Collect metrics

This Week:

  * [ ] Add docs about Grafana, adding nodes

  * [ ] Continue to rewrite tps-bench (expose the bench metrics and system metrics)

  * [ ] Research testplan, or maybe other frameworks

@chuijiaolianying

Last week

 * [] learning Rust and blockchain
 
 This Week
 
 * keep learning
 * [try testground](https://github.com/nervosnetwork/ckb-internal/issues/636)

---
### Plan
