# CLAUDE.md

Instructions for Claude Code in this repository. Read this first, then the docs it points to.

## What this is

PropertySmith is a working name, built by NHMiller Enterprises. It's an agentic platform for real estate brokerages and property management firms: leads to closing, and owner to resident. It's multi-tenant from day one, and runs on the StaffSmith foundation (`nhmillerbusiness/staffingplatform`).

**This repo is design history.** Real estate is built as modules on the StaffSmith platform, in `nhmillerbusiness/staffingplatform`, folder `realestate/`. There's one deployment and one database, with a schema per module (ADR 0001; StaffSmith ADR 0023). Its docs move there with design-v0.9.10; edit them there, not here.

## Source of truth (read in this order)

1. `docs/working-assumptions.md`: principles and build defaults. **Binding.**
2. `docs/concept.md`: what the platform does (edited as a Claude Doc, committed per version).
3. `docs/roadmap.md`: build order. Work on the current phase unless told otherwise.
4. `docs/adr/`: architecture decision records.
5. `docs/QUESTIONS.md` and `docs/handoffs.md`.

If two documents conflict, `working-assumptions.md` wins, then the newest ADR. Point out the conflict; don't resolve it silently.

## Non-negotiable rules

- **Tenant ID on everything.** Every tenant-owned table, S3 object key, queue message, event, vector and memory item carries `tenant_id`. Postgres row-level security enforces it. The tenant comes from the authenticated token or the workflow context, never from a request URL or body.
- **People decide consequential matters.** No agent, owner, resident or partner may directly set an outcome that does any of these:
  - approves, denies or conditions a rental applicant;
  - sets or changes rent, a fee, a deposit deduction or a payment plan;
  - starts an eviction or any legal notice;
  - disburses money from a trust account;
  - submits, accepts or counters an offer;
  - waives a contingency;
  - publishes a listing.

  These go through the decisions queue and wait for a named staff member.
- **Fair Housing by design.**
  - Listings, ads, messages and screening criteria pass a Fair Housing wording check.
  - Agents never describe a neighborhood by who lives there.
  - Ad audiences are never targeted by protected class.
  - Reasonable accommodation requests always go to a person.
  - Screening uses the property's written criteria, the same for every applicant.
- **Licensed activity stays with licensees.** Digital workers schedule, inform and draft. They never negotiate, advise on price or terms, or interpret a contract.
- **Trust money is separate.** Client and resident funds sit in trust ledgers, never mixed with the firm's own. Reconciliations are signed by a person.
- **Legal wording is a marked placeholder until counsel approves it.** That covers leases, notices, disclosures, adverse action letters and agreements.
- **Every model call goes through the AI gateway.** Every agent action is logged: prompt, model and version, tools called, output, and the linked decision.
- **No secrets in the repo; no PII in application logs.** Secrets live in AWS Secrets Manager. Logs carry ids, never names, contact details or financial data.
- **Vendor services sit behind thin internal interfaces with fakes:** MLS, screening, payments, syndication, e-signature, messaging.

## Cost and override protocol

The same as StaffSmith (see its CLAUDE.md, "Cost and override protocol"). Stewardship of resources comes first.

**Defaults** that need no approval: Lambda, Step Functions, SQS, EventBridge, S3, Aurora Serverless v2 scaling to zero, and Haiku or Sonnet models.

**Stop and ask Nathan first**, stating the monthly cost or the lock-in, before adding any of these:

- an always-on resource;
- a new paid service (MLS access, screening bureau, payments provider);
- a vendor dependency that core logic would rely on.

Real estate runs in StaffSmith's AWS accounts, under the same budgets (ADR 0023).

## Working with the Claude app

The same collaboration protocol as StaffSmith:

- Design arrives as bundles in `import/` with a `MANIFEST.md`.
- Questions go in `docs/QUESTIONS.md`, with "Default applied" when they're reversible.
- Completed and Divergence entries go in `docs/handoffs.md`.
- Never delete: move files to `_to_delete/YYYY-MM-DD/<path>` and list them in `_to_delete/INDEX.md`.

Autopilot isn't set up in this repo yet.

## Commands

None yet. They arrive with the skeleton (roadmap, Phase 1).
