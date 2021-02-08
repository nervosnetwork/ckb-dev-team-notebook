# CKB Dev Meeting Mon, Aug 17, 2020

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

#### Retrospective

* **Presenter**: Ian Yang
* **Time Allowed**: 20min
* **Topic**:
    * Quake, Snappy Postmortem
    * Dingwei, Data Hash Syscall Postmortem
    * Quake, Integration test failures retrospective

#### OKR Kickstart

* **Presenter**: Ian Yang
* **Time Allowed**: 10min
* **Topic**: Introduction to OKR

---
## Meeting Notes

---
### Progress Update

@doitian

Last Week:

* [G] Design fee estimate algorithm for CKB
* [Y] Research fee bumping
    * I have surveyed related articles but haven't summarized them yet. I have listed the related notes in this list: https://www.evernote.com/pub/doitian/ckbfeemechanismdesign#st=p&n=65c66969-e334-4802-8b13-0b6236e83151
    
This Week:

* Summarize fee bumping and write an essay about it.
* Write an essay about the best practices to manage transaction statuses and utxos.
* Set team OKR

@quake

Last Week:

- [ ] lightnode UI 预期还要6～7个工作日完成

This week:

- [] lightnode UI 
  * debug and test
  * try build lightnode client on android
@zhangsoledad

Last Week:
* [G] add some test cases 
* [G] freezer snappy
* [Y] relay tx by wid
* [R] audit code 


This week:
* Finish relay tx refactory
* refactory ResolevdTransaction


@driftluo

Last Week:
- [x] Release tentacle  and update ckb tentacle
- [x] Go ping finished
- [x] Rewrite ckb ping (need review)

This week:
- Discovery on Go
- According to go implementation, adjust ckb discovery as needed
- Try to remove ckb `Both` protocol

@yangby-cryptape

Last Week:
- [Y] Upgrade ckb-bench and the bench bot.
  - New bench tool has some issues, already had a discussion with Guozhen.
  - [Y] Replace the old bench tool.
- [G] Refactor app-config so it does not depend on services.
- Metrics for Chain Freezer.
  - Re-assign to Dingwei.
- [Y] Better RocksDB options for HeaderMap.
  - [G] Add some metrics.
  - [Y] Compare several options.

This Week:
- Upgrade ckb-bench and the bench bot.
- Better RocksDB options for HeaderMap.

@keroro520

Q3 Major Tasks:

* Run a staging network, including transactions generator and system monitor. It is like an internal-use testnet network.
* Run several known test scenarios on testground.
* Refactor integration, make it more programable and readable.

Last Week:

Last Week:

  - [Y] tps-bench runs on staging network(I set up 3 nodes on aws). But I want to improve the usability and add some more related features(part of those come from boyu).
  - [R] Extract commonly used behaviors of integration-tests, to improve the programmability and readability.

This Week:

  - Debug why tps-bench get `TransactionFailedToResolve` error on multiple-node network. And continue replacing the old tps-bench.
  - Extract commonly used behaviors of integration-tests, to improve the programmability and readability.

@chuijiaolianying

Last Week:

* [G] Prefix integration test log #774 
* [G] node with time error in aggron network #742 
* [Y] ckb-bench doc #776 
    * read ckb-bench code, but not finish the doc yet
* [R] assert events via log #758 
    * didn't spend lot time on this issue last week
    
This Week:
* assert events via log #758
* ckb-bench relate issue #776
* adjust uncle rate in aggron network #789 

---
### Plan
