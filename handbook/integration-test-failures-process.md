# Integration Test Failures Process

We run the integration 7x24, all failed test cases will be posted to [sentry](http://sentry.nervos.org/ckb/ckb-integration/).

Alerts are also sent to the Github repository [CKB Dev Alerts](https://github.com/nervosnetwork/ckb-dev-alerts) as issues if the test cases failed

* more than 2 times in an hour,
* or more than 5 times in a week.

Every week, we'll pick the most occurred failed test case to fix. We have one engineer who is on duty as the devops owner every week. The devops owner is responsible to troubleshoot why the test case fails and try to fix it. Whether the test case has been fixed or not, the devops owner must submit a retrospective. The whole team will discuss based on the retrospective report and propose suggestions if the test case are not fixed yet.

If the test case is not fixed, it will be deferred to the next week. The test case can only defer once. If it is still not fixed in the next week, the test case must be disabled. Once there are no failed test cases, we will pick disabled test cases to work on.

The board [Integration Test Failures](https://github.com/nervosnetwork/ckb-dev-alerts/projects/1) manages all the failures, and uses columns for the different states:

* To do: new failures
* Troubleshooting: the devops owner is working on it
* Disabled: the test case is disabled
* Refactoring: the test case requires efforts to refactor
* Done: fixed
