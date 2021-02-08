# CKB Dev Responsibilities and Paths

This document categorizes CKB Dev Team responsibilities into paths. 

We'll use paths as a guideline to reduce context switching and help engineers to improve their efficiencies.

At the top level, we can split paths into four layers.

1. Infrastructure Layer
2. Core Layer
3. Interface Layer
4. Apps Layer

Each layer is the foundation of the latter layer.

![image](https://user-images.githubusercontent.com/35768/82651619-f7620600-9c4e-11ea-841e-c510db09f4d1.png)

## Infrastructure Layer

This layer is the foundation and usually can be shared with other teams.

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Al%3Ainfrastructure)

### Network

* P2P framework development. Explore ways to improve security, latency and performance of the framework.
* Design and deploy large scale environments to study CKB network's behaviors.
* Improve CKB's network stack based on requirements of different running environments.
* Implement or prototype networking optimization ideas.

Related paths:

* Infrastructure / Performance
* Infrastructure / DevOps
* Core / P2P Protocols

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Anetwork)

### Performance

* Design and develop benchmarks/workloads to identify performance issues.
* Design and build automatic performance diagnosis & analysis tools.
* Implement or prototype optimization ideas
* Research next generation architectures to improve the performance.

Related paths:

* Infrastructure / DevOps
* Core / Architecture

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Aperformance)

### DevOps

* IT operations: orchestration, cloud environments management, credentials management.
* Automation tools: orchestration, deployment, logs and metrics collection, alerts, outages tracking, security scanning, continuous integration and delivery.
* Incidents management: on-call, troubleshooting, retrospective.

See more in [Google SRE](https://landing.google.com/sre/books/).

Related paths:

* Infrastructure / Performance
* Infrastructure / Network
* Infrastructure / Test

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Adevops)

### Test

* Design, build and automate test cases.
* Build test tools and methodologies: chaos test, fuzz test, deterministic test, mocks, async and distributed system test.
* Use tools to reason concurrent and distributed system such as TLA+.

Related paths:

* Infrastructure / DevOps

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Atest)

### VM

* RISC-V
* Assembly level optimization.
* Expert in fundamental computer science: computer architecture, compilation, programming language design and etc.

Related paths:

* Infrastructure / Performance
* CKB / Chain

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Avm)

## Core Layer

This layer is major responsibility of the CKB Dev Team.

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Al%3Acore)

### Pool

Pool manages to-be-committed transactions.

* Design the data structure to index transactions.
* Support various strategies to sort transactions.
* Add features to support transaction generators.
* Expose interfaces to allow inspecting and managing the transactions in the pool.

Related paths:

* Interface / API

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Apool)

### Chain

Chain is the core in the core layer.

* Design and implement the consensus. Make trade offs among performance, security and decentralization.
* Design and implement the cell model.
* Improve the performance to execute consensus.

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Achain)

### Storage

* Design the storage hierarchy. Choose the right database and cache technology stack.
* Design and run storage benchmark. Understand the data flow and access patterns. Find out the bottlenecks.
* Design the database structures and indices.

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Astorage)

### P2P Protocols

* Design P2P protocols for CKB.
* Sync/relay performance tuning.
* Design efficient protocols to fully utilize the network bandwidth.
* Design mechanisms to resist various network attacks.

Related paths:

* Infrastructure / Network

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Ap2p-protocols)

### Architecture

* Rust expert.
* Design the architecture for a high performance asynchronous application.
* Summarize and apply the Rust patterns and best practices.
* Ensure the testability from the architecture.

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Aarchitecture)

## Interface Layer

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Al%3Ainterface)

### API

* Develop APIs for wallets, miners, chain explorers and developers.
* Develop APIs for test, automation and troubleshooting.
* Provide detailed and up-to-dated API documentation.

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Aapi)

### SDK

* CKB as lib
* Reusable crates

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Asdk)

### Cli

* CKB Cli

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Acli)

### System Scripts

* Design essential lock and type scripts.
* Design common libraries to be used in lock and type scripts.

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Asystem-scripts)

## Apps Layer

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Al%3Aapps)

### Governance

* Design fork mechanism.

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Agovernance)

### Apps Protocols

* Research what CKB should provide to support layer 2.
* Design and build tools for layer 2, such as live cells indexer.
* Research and implement protocols for the ecosystem, such as light client, lighting network, open transactions and etc.

[See issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3Am%3Aapps-protocols)
