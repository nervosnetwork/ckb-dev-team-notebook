# CKB Release Plan

Assume that the current version is v0.29.0, and the next version is v0.30.0.

* Create branch rc/v0.30 on the first Monday of the next month. Freeze the code and deploy the RC version to half nodes in both testnet and mainnet.
* Release v0.30.0 on the third Monday of the next month. Deploy the release to all nodes in both testnet and mainnet.

Before v0.30.0 is released, bug fixings must backport to both rc/v0.30 and rc/v0.29 and release a new patch version such as v0.29.1.

After v0.30.0 has been released and before rc/v0.31 is created, bug fixings only backport to rc/v0.30 and release a new patch version such as v0.30.1.
