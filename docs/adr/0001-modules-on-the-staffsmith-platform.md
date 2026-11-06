# 0001: Real estate as modules on the StaffSmith platform

- Status: Accepted
- Date: 2026-11-05
- Decider: Nathan Miller (RE-07)

## Decision

Real estate (brokerage and property management, working name PropertySmith) is built as modules on the same platform as StaffSmith:

- one codebase in `nhmillerbusiness/staffingplatform`, folder `realestate/`;
- one deployment;
- one database. Real estate data goes in a `realestate` schema, and trust accounting and payments in a `trust` schema;
- shared records across modules: contacts, companies, activities, tasks, the Inbox, comms and decisions.

Staffing work comes first; real estate is backfill.

The full record is StaffSmith's [ADR 0023](https://github.com/nhmillerbusiness/staffingplatform/blob/main/docs/adr/0023-one-platform-with-product-modules.md).

## Consequences

- This repo is design history. Its docs move to `staffingplatform/realestate/docs/` (design-v0.9.10) and are edited there.
- Nathan archives this repo on GitHub once they've landed.
