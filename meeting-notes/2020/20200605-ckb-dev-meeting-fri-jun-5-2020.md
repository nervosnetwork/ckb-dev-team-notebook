# CKB Dev Meeting Fri, Jun 5, 2020

## Agenda

### Details

* **Project**: CKB
* **Time**: 50min, at 1:30pm
* **Meeting Goal**: Seminar, Brainstorm
* **Meeting Room**: https://meet.google.com/gix-ipdy-efr
* **Host**: ian
* **Attendees**: CKB Dev Team, Jan

### Agenda Items

#### Brainstorm for Jun

* **Presenter**: Ian
* **Topic**: Ideas about what to do in Jun
* **Time Allowed**: 30min

By Modules:

* Interface Layer
    * API [19 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Aapi)
        * Better errors
        * Better documentation
        * Add more inspection RPC methods
    * SDK [5 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Asdk)
    * Cli [3 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Acli)
    * System Scripts [3 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Asystem-scripts)
* Apps Layer
    * Governance [7 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Agovernance)
        * Fork
    * Apps Protocols [6 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Aapps-protocols)
        * Light client

#### Chain Sync Simulation Test

* **Presenter**: Ian
* **Topic**: How to improve the simulator 
* **Time Allowed**: 30min

See [repo](https://github.com/nervosnetwork/sync-scheduler-simulation-test).

---
## Meeting Notes

Brainstorm items will be merged into [the last meeting](https://github.com/nervosnetwork/ckb-internal/pull/628).

### Simulation Test

* [ ] Collect latency data by peer
* [ ] Run new sync scheduler in China mainland and Europe.
