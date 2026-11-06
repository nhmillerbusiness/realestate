# Working assumptions

v0.1 · Nov 5, 2026 · from the Claude app, for Nathan to confirm

These are binding for Claude Code. Change them only through Nathan, and record each change as an ADR.

## Principles

1. **Stewardship first.** Pay-per-use services before always-on ones. Small costs don't slow the work, and big ones go to Nathan first (the StaffSmith protocol).
2. **Multi-tenant from the first line.** The first firm is tenant one of many.
3. **Digital workers do the work; people decide.** Every consequential outcome passes through the decisions queue (see CLAUDE.md for the list).
4. **Fair Housing and FCRA are design constraints, not features.** The wording check, written screening criteria, paired-applicant eval gates and person-made decisions ship with the first leasing feature, not after it.
5. **Reuse before rebuild.** Anything StaffSmith already does (tenancy, gateway, decisions, action log, Inbox and tasks, comms, templates, rules, KPIs, custom objects, integrations hub, portal, operator console, commissions) comes from the shared core, not a copy.
6. **State-aware by configuration.** Trust accounting, deposits, late fees, notice periods, license limits and MLS rules vary by state. They live in per-state configuration, starting with one state (RE-05).

## Platform defaults (carried over from StaffSmith, until an ADR here says otherwise)

| Area | Default | StaffSmith reference |
| --- | --- | --- |
| Cloud | AWS, in PropertySmith's own accounts | Working assumptions |
| Infrastructure as code | AWS CDK in TypeScript | ADR 0001 |
| Backend language | TypeScript (a narrow Python lane for offline analysis) | ADR 0002 |
| Frontend | React + Vite, static, behind Cloudflare | ADR 0003 |
| Database | Aurora Serverless v2 (PostgreSQL) with the Data API, scaling to zero | ADR 0007 |
| Data access and migrations | Kysely; plain SQL migrations | ADR 0005 |
| Vectors | pgvector | ADR 0006 |
| Sign-in | Amazon Cognito | Working assumptions |
| Email and calendar | Microsoft 365 (Google Workspace later) | C13 |
| Finance | QuickBooks Online for the management company's own books, plus a trust ledger in PropertySmith | C16 |
| Texting | AWS End User Messaging SMS, fake adapter until launch | ADR 0018 |
| Models | Claude through the AI gateway; Haiku and Sonnet by default | Agents and AI gateway |

## Scope assumptions (to confirm: RE-01 to RE-05)

- **Market:** residential only. Single-family and small multifamily.
- **Firms:** small and mid-sized, often doing both brokerage and property management.
- **Order:** property management first, then brokerage.
- **First state:** Arizona.

## Not decided

- **How the shared core gets out of StaffSmith** (RE-07): its own repo of packages, or a monorepo, or published npm packages. It needs an ADR in both repos.
- **The product name** (RE-06).
- **Pricing** (concept, "Pricing ideas"), which waits on the StaffSmith digital worker pricing conversation.
