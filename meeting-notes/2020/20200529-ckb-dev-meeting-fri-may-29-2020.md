# CKB Dev Meeting Fri, May 29, 2020

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

* **Topic**: Ideas about what to do in Jun
* **Time Allowed**: 50min

* Infrastructure Layer
    * Network [3 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Anetwork)
    * Performance [9 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Aperformance)
        * TPS Bench
        * Sync
        * Memory
    * DevOps [21 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Adevops)
        * Testbed Environment
        * Memory
        * Metrics
        * Alert
        * Inspection RPC
    * Test [18 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Atest)
        * Integration Test
        * Testbed Environment
        * Chaos, fail
        * Block Sync
        * TLA+
    * VM [2 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Avm)
* Core Layer
    * Pool [11 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Apool)
        * Collect Requirements
        * Add more features and provide more RPC methods
    * Chain [11 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Achain)
        * Header first
    * Storage [8 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Astorage)
        * Chain Freezer
        * Cells cache
    * P2P Protocols [34 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Ap2p-protocols)
        * Sync
        * Relay
        * Middleware
        * Header first
        * Peers management
    * Architecture [15 issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Aarchitecture)
        * P2P Middleware
        * CKB as lib
        * Orphan pool resource contention
        * Bad smells
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

### Meeting Notes

#### Status Update

* @zhangsoledad Cell storage improvements. On 100m blocks, the process time decreases from 202s to 170s.
* @driftluo The existing P2P should already support checking the status of send buffers, but read buffer is not supported.

#### Brainstorm

* DevOps
    * Use Prometheus push to collect test results
    * Collect TPS Bench memory and CPU information
        * CPU/memory increases
            * start/end/peak
    * Way to show the report
        * Grafana dashboard
        * Export PDF
    * Continuous Delivery
        * We need to build binary for deployment.
            * Enable debug symbol table
* Test
    * Enable fail points in staging.
    * Compilation time is much longer than the test time
        * Copying target dir is faster than linking
        * Pre-build ckb-test
        * Remove unnecessary dependencies from ckb-test
        * If ckb and ckb-test use different compilation flags and share the target directory, some c library won't be recompiled using the new flags.
    * Integration test alerts
* Performance
    * It spends a lot of time to support orphan transactions
    * Removing transaction orphan pool may affect relay. A node may receive a transaction before its dependencies from the relay protocol.
* API
    * Should we deprecate ckb RPC indexer?
    * There's a bug in ckb builtin indexer, it creates an empty database even when it is disabled.
    * Package ckb-indexer in release
* Architecture
    * CKB as lib
    * Database error
    * Database interface is not flexible
    * Header-first sync
    * Async
        * Even Future and Tokio are not fully compatible.
    * The upper layers depend on the store layer details.
* Storage
    * Parity DB write 3x, read 2x
        * Specialized database for ethereum
    * RocksDB override key hash method.
* P2P Protocols
    * Wrap existing code as legacy and rewrite the protocols.
    * Async/await API
    * Refactor into P2P/Protocols/Core layers
* Governance
    * Fork
        * Add syscall to returns cycles
* API
	* 对比 Bitcoin/Ethereum RPC
	* Deprecate RPCs
		* JSONRPC deprecation features
		* Get cells by lock hash
		* Built-in indexer
* SDK
	* 整理错误，废弃 failure
* Apps Protocols
	* Indexer via P2P
	* Light client integration
	* Reference: libp2p spec pub/sub, ghost pub/sub

#### Process

We'll tag tasks by colors:

* Blue: improvements
* Red: aggressive features
* Pink: between Blue and Red

### Action Items

* @driftluo Benchmark specification and setup, create a wiki, add a link in the PR comment.

