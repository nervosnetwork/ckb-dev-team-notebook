# Dependencies Upgrade Guideline

For crate upgrade which does not require changing `Cargo.toml`:

*   Wait for dependent bot or submit a PR which includes the crate change log, release notes and the diff between the old version and new version.
*   Follow the normal PR approval policies.

For crate upgrade which does require changing `Cargo.toml` and the Rust toolchain upgrade.

*   Propose a request to upgrade the crate or toolchain. Present the reason why we should upgrade.
*   The upgrade PR cannot be merged in the current sprint, it must be postponed to the next sprint.
