# CKB Dev Meeting Mon, Jul 6, 2020

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

N/A

---
## Meeting Notes

---
### Progress Update

@doitian

Last week

* [x] Q3 Plan
* [x] Invest why integration fails in Windows CI

This week

* [ ] Discuss COs in Q3
* [ ] Refactor RPC errors
* [ ] Header doc

@quake

* Continue Channel prototype review 

@zhangsoledad

Last week
* [x] fix too-far-ahead block get banned
* [x] fix proposal table issue
* [x] freezer improvement (repair test, fail points, truncate, etc.)

This week
* [ ] migration: mark branch, clean forks.
* [ ] independent migration refactory
* [ ] redesign transaction resolve, split orphan tx pool

@driftluo

Last week
- [x] tentacle-go example is consistent with Rust and can communicate normally
- [x] tentacle improvement pr

This week
- trying to implement a channel with priority, now the implementation is a bit dirty（Rust）
- test on tentacle-go

@yangby-cryptape

* Cleanup PR
* Header map persistent discussion with @quake
* Survey why Header map cache misses

Blocking:

* Test environment meeting with Muta
* Headermap storage implementation

@keroro520

* Experiment Testground
* Research tools suggested by Muta

@chuijiaolianying


Last week

* [ ] Testground research
* [ ] add integration test cases doc
* [ ] learn ansible, read ckb-devops/net-test relate code

This week

* [ ] Finish integration doc issue
* [ ] https://github.com/nervosnetwork/sync-scheduler-simulation-test/issues/6

---
### Plan
