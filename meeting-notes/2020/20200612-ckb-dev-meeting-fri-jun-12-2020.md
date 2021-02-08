# CKB Dev Meeting Fri, Jun 12, 2020

## Agenda

### Details

* **Project**: CKB
* **Time**: 50min, at 1:30pm
* **Meeting Goal**: Seminar, Brainstorm
* **Meeting Room**: https://meet.google.com/gix-ipdy-efr
* **Host**: ian
* **Attendees**: CKB Dev Team, Jan

### Agenda Items

#### Triage Issues and Review PRs

* **Presenter**: Ian
* **Time Allowed**: 50min

Links:

* [Triage issues](https://github.com/nervosnetwork/ckb-internal/issues?q=is%3Aissue+is%3Aopen+label%3As%3Atriage)
* [Review PRs](https://github.com/nervosnetwork/ckb/pulls?q=is%3Apr+is%3Aopen+created%3A%3C2020-06-02)

---
## Meeting Notes

┌ https://github.com/nervosnetwork/ckb/issues/2067


@quake plans to give a better distribution models after @keroro520 has collected new metrics.

┌ https://github.com/nervosnetwork/ckb/issues/2036

This does not cover indexer DB.

┌ https://github.com/nervosnetwork/ckb/issues/2082

* [ ] @driftluo We need documents about `Both` and `Callback`
    * What's the recommended default method?
    * What's the limit of the default method?
    * When we should use the alternative method.


┌ https://github.com/nervosnetwork/ckb/issues/1988

* Change the headers sync time out 362 seconds to a smaller value, such as 10s. Check whether the node will switch to another peer smoothly.
* [ ] @yangby-cryptape Refactor the function to pass linter instead of allowing cognitive_complexity.
* What to do when we finish the headers sync with a peer when it first returns a headers response with less than 2000 headers and its best known header is not fresh according to the wall clock?

┌ https://github.com/nervosnetwork/ckb/issues/2090

* [ ] @keroro520 Please add some doc in `docs/ckb-core-dev.md` about how to enable this feature.

┌ https://github.com/nervosnetwork/ckb/issues/2064

* Add a test RPC to create a block from pool and connect it to the chain.
* [ ] @keroro520 Refactor chain service to simplify the truncate method. Call for help from @zhangsoledad
    * The code is a bit too complex. The chain service should provide a interface to allow setting any stored block as tip.
    * Also it is better to leave the stored blocks untouched. Once a node receives a stored block, and it has better cumulative difficulty, the chain service should set tip to this new block instead.

┌ https://github.com/nervosnetwork/ckb/issues/2042

* [ ] @keroro520 The feature is not available in Windows, it should return an error for Windows.

┌ https://github.com/nervosnetwork/ckb/issues/2110 https://github.com/nervosnetwork/ckb/issues/2111

* Remove estimate RPC related code, only leave a dummy implementation which always return the error like what the mainnet does. (#661)

┌ Headers Verification has too many dependencies

The headers verification is in the same crate with full block verification, which in turns depends on the whole storage layer implementation.

@quake will document the issue in details in a new issue.

This also a new evident that we have two many code depends on the storage details, instead of an interface.
