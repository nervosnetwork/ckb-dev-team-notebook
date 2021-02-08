# Integration Test Failures Process

We run the integration 7x24, all failed test cases will be posted to [sentry](http://sentry.nervos.org/ckb/ckb-integration/).

Alerts are send to telegram channel [CKB Dev Alert](https://t.me/joinchat/AAAAAEtQp3n_ieZ6-PD5oA) if the test cases failed

* more than 2 times in an hour,
* or more than 5 times in a week.

Alerted test case will has its own issue in the ckb-internal repository, which a shared link to the sentry event. See an example of the test case [pool resurrect](https://github.com/nervosnetwork/ckb-internal/issues/743).

Every week, we'll pick the most occurred failed test case to fix. We have one engineer who is on duty as the devops owner every week. The devops owner is responsible to troubleshoot why the test case fails and try to fix it. Whether the test case has been fixed or not, the devops owner must submit a retrospective. The whole team will discuss based on the retrospective report and propose suggestions if the test case are not fixed yet.

If the test case is not fixed, it will be deferred to the next week. The test case can only defer once. If it is still not fixed in the next week, the test case must be disabled. Once there are now failed test cases, we will pick disabled test cases to work on.

The board [D: Integration Test Failures](https://github.com/nervosnetwork/ckb-internal/projects/43) manages all the failures, and uses columns for the different states:

* To do: new failures
* Troubleshooting: the devops owner is working on it
* Disabled: the test case is disabled
* Refactoring: the test case requires efforts to refactor
* Done: fixed
