# PropertySmith (working name)

A multi-tenant, agentic platform for real estate brokerages and property management firms, built by NHMiller Enterprises on the StaffSmith foundation.

Digital workers do the routine work: leasing inquiries, maintenance triage, transaction checklists, owner statements. People make every decision that affects someone's housing, money or legal position.

**Status:** concept (v0.1, Nov 5, 2026). There's no code yet. The build starts once the open questions in [`docs/QUESTIONS.md`](docs/QUESTIONS.md) (RE-01 to RE-05) are answered.

## Read in this order

1. [`docs/concept.md`](docs/concept.md): the concept. It covers the market, the modules, the digital workers, the compliance guardrails, integrations, pricing and build order.
2. [`docs/working-assumptions.md`](docs/working-assumptions.md): the principles and the defaults carried over from StaffSmith.
3. [`docs/roadmap.md`](docs/roadmap.md): the build order as checklists.
4. [`docs/QUESTIONS.md`](docs/QUESTIONS.md): the open questions for Nathan.
5. [`docs/handoffs.md`](docs/handoffs.md): requests and completions between the Claude app and Claude Code.

## Relationship to StaffSmith

PropertySmith is a separate product and repo for now. It will run on StaffSmith's shared core (tenancy, the AI gateway, the decisions queue, the agent action log, comms, templates, rules, the integrations hub, the portal and the operator console), once that core is extracted into packages.

Until then, this repo holds only design. StaffSmith lives in `nhmillerbusiness/staffingplatform`.
