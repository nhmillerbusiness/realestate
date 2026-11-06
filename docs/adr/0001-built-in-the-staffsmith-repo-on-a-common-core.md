# 0001: Built in the StaffSmith repo, on a common core

- Status: Accepted
- Date: 2026-11-05
- Decider: Nathan Miller (RE-07)

## Decision

PropertySmith is built in `nhmillerbusiness/staffingplatform`, in its `propertysmith/` folder. It runs on the common core in that repo's `packages/`.

The full record is StaffSmith's [ADR 0023](https://github.com/nhmillerbusiness/staffingplatform/blob/main/docs/adr/0023-one-repo-for-the-common-core-and-products.md). It covers:

- the layout;
- the dependency rule;
- separate databases, AWS accounts and CDK apps;
- per-product checks;
- extracting core pieces only when PropertySmith needs them.

## Consequences

- This repo is design history. Its docs are copied to `staffingplatform/propertysmith/docs/` (design-v0.9.10), and they're edited there from then on.
- Nathan archives this repo on GitHub once the copy has landed. Archiving is reversible.
