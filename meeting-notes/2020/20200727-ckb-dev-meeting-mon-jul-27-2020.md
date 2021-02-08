# CKB Dev Meeting Mon, Jul 27, 2020

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

##### Discussion Items

* `getblockstats` in [#729](https://github.com/nervosnetwork/ckb-internal/issues/729)
* Discuss the plan of [#682](https://github.com/nervosnetwork/ckb-internal/issues/682)
* Align works with [Q3 milestone](https://nervos.quip.com/tIqKAblsbOeA/CKB-Q3-Project-Break-Down#SBZACAk3V6q)

---
## Nervos Briefing

### Dev Tools

[@xxuejie: SUGGEST HERE]

### MAKE

* ckb oracle bridge [→](https://github.com/duanyytop/ckb-oracle-bridge/issues/1)
* light node of CKB [→](https://github.com/nervosnetwork/ckb-explorer-internal/issues/686)
* Mining pool stats
* Replace tauri with electron in keypering
* Research on ledger nano integration with Neuron [→](https://github.com/nervosnetwork/neuron-internal/issues/1213)

### Research

* Design zkUDT
* review a paper about multi-signature for IEEE Transactions on Information Forensics and Security
* research multi assets on MW

---
## Meeting Notes

---
### Progress Update

@doitian

Last week

* Fee mechanism research
    * [x] Write a document about how ckb prioritizes transactions currently
    * [.] Research different ways to estimate fees

This week

* Continue fee mechanism research
    * Fee estimate methods comparison
    * Research how to improve CKB to support Child-Pay-For-Parent and Replace-By-Fee.
* Research compact block filtering
* Research feasibility to adjust time using the p2p network

@quake

Last Week

* Review channel prototype ruby code, add unit test

* Add more RPC (generate_block)


This Week 
* Add more RPC
    - move `add_node` / `remove_node` rpc to network module

    - add more fields to `local_node_info`

    - add more fields to `get_peers`

* light client UI


@zhangsoledad

Last week
* [.] redesign transaction resolve and transaction orphan pool
* [ ] Research rust multiple index container

This week
* [ ] transaction resolve with cell storage refactory PR
* [ ] tx-pool multiple index container

@driftluo

Last Week

- [x] Rewrite the tentacle poll (merged)
- [x] Rewrite the tentacle buffer (need review)
- identify go

This Week

- Hope Tentacle can be released
- Protocol impl on go
- `sync state` rpc, if there is no opinion, start to impl

@yangby-cryptape

Last week
- [x] [Logger supports multiple output target, each target can configure different filters.](https://github.com/nervosnetwork/ckb-internal/issues/724)
- [ ] [Embedded metrics service](https://github.com/nervosnetwork/ckb-internal/issues/602)
- [ ] [Ensure CKB can run on host with only 800m memory](https://github.com/nervosnetwork/ckb-internal/issues/689)

This week
- [ ] **Block** PRs for Rocksdb are required, to continue PR about `Memory`.
- [ ] [Embedded metrics service](https://github.com/nervosnetwork/ckb-internal/issues/602)
  - [ ] Replace current metrics part.

@keroro520

Last Week

  - [ ] Run staging network based on ckb-devops-configs(also add tps-bench into ckb-devops)
  - [x] Debug and fix integration test failure "pool_resurrect"
  - [ ] Continue write ckb-plan based on testground. Most of time are spending in rewrite event/metrics/logger modules.

This Week

  - [ ] Review integration test PR
  - [ ] Continue to run staging network based on ckb-devops-configs(also add tps-bench into ckb-devops)
  - [ ] Continue write ckb-plan based on testground

@chuijiaolianying

Last Week

* [ ] refactor integration test

This Week

* [ ] continue integration test refactor
* [ ] research time offset in integration test

---
### Plan
