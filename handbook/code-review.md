# Code Review Developer Guide

We follow the [Google's Code Review Developer Guide](https://google.github.io/eng-practices/review/).

Our extensions and highlights:

* Prioritize code review. Especially if someone requests the review in the Telegram group, take it as the highest priority.
* Use the eye emoji reaction (👀) as an indication that you are reviewing the PR. If the review will take more than one day, leave a comment about your estimated finish date.
* Dependency upgrade must include the change log and changes comparison (e.g. https://github.com/nervosnetwork/ckb/compare/v0.12.0...v0.12.1 )
* Every PR requires at least two approvals. At least one reviewer is the [code owner](https://docs.github.com/en/free-pro-team@latest/github/creating-cloning-and-archiving-repositories/about-code-owners).
* The PR changes must be covered by test cases. If the PR fixed a bug, it must reproduce the bug via a test case.
