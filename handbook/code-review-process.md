# Code Review Process

This process help us to prioritize code review.

## Module Owners

To ensure there are enough resources to do code review, the team leader must ensure that every module has at least three developers who are are familiar with the module.

When there are no enough developers, the team leader is responsible to train the existing developers or hire new ones.

See [#863](https://github.com/nervosnetwork/ckb-internal/issues/863) for the current assignments table.

## CDIP (CKB Dev Improvement Proposal) Reviewers

If a feature is complex and large, it is required to publish a PR in ckb-internal to initialize the discussion. Please use script `bin/create-cdip` to create the file.

Two reviewers will be assigned as assignees of the CDIP PR. The two reviewers and the CDIP owner constitutes a small team and will schedule a series of design review and code review meeting.

## PR Call For Review

If your PR is urgent or the review is too slow and has blocked your work, please send a message tagging `#cfr` (acronym of Call For Review). The team leader will add it to the review queue.

We'll use the [CKB Pull Requests Board](https://github.com/orgs/nervosnetwork/projects/18) as the review queue.

* We'll focus at most 4 PRs at one time and they are listed in the column `👀 In review (Max 4)`. If you have an urgent PR but this column is full, please help to review the pull requests in the column first.
* When the column is full, extra PR review requests will be queued in the column `😴 Awaiting Review`.
* If a PR is waiting for further changes, please move the PR to `🚧 In progress` so it will not block the reviews for other PRs.

## Plan the Review

Review is an important part of our work. When we plan our work, we must spare enough time for review.

* We'll add a section about review in our planing, brainstorming and retrospective meeting.
* We'll add a section about review in our weekly meeting.
