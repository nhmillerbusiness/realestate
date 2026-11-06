# Roadmap

Build order from `docs/concept.md`. Items marked `(waiting: RE-nn)` wait on Nathan.

## Phase 0: Decisions

- [x] Scope: residential and commercial, all portfolio sizes, both modules together (Nathan, Nov 5, 2026)
- [x] First state: Arizona (Nathan, Nov 5, 2026)
- [ ] First firm (RE-04: coming)
- [ ] Product name (waiting: RE-06)
- [x] ADR 0001: one repo, on a common core (StaffSmith ADR 0023; Nathan, Nov 5, 2026)
- [ ] PropertySmith's AWS accounts and budgets, created by Nathan

## Phase 1: Shared core and skeleton

- [ ] Core pieces extracted from `services/ats` into `packages/` as PropertySmith needs them, StaffSmith's checks green after each
- [ ] `propertysmith/` skeleton in the StaffSmith repo: its CDK app, apps and services workspaces, `propertysmith/scripts/check.sh`, the lint boundary rule, the cost guards
- [ ] Tenant creation, sign-in, the decisions queue and the AI gateway wired to the core
- [ ] A demo tenant with sample owners, properties, units, residents and vendors

## Phase 2: Property management, leasing (built alongside Phase 4, RE-02)

- [ ] Owners, management agreements and the owner portal
- [ ] Portfolios, properties and units; compliance attributes such as lead-based paint for pre-1978 housing
- [ ] Vacancy listings with the Fair Housing wording check; syndication adapter with a fake
- [ ] The leasing assistant: inquiries, tours, applications
- [ ] Written screening criteria per property; screening adapter with a fake; the FCRA adverse action flow; the screening reviewer
- [ ] Applicant decisions in the decisions queue; paired-applicant eval gate
- [ ] Leases from state templates (placeholder wording), e-signature, renewals

## Phase 3: Property management, operations and money

- [ ] Resident accounts: charges, payments adapter, late fees by state rule, deposits
- [ ] Maintenance: requests, triage, vendor dispatch within owner limits; the maintenance coordinator
- [ ] Inspections on the mobile app; the inspection assistant
- [ ] Trust ledger per bank account; reconciliation signed by a person; owner statements and disbursements through the decisions queue; the accounting assistant
- [ ] QuickBooks for the management company's own books

## Phase 4: Brokerage (built alongside Phases 2 and 3, RE-02)

- [ ] Leads, routing, the lead concierge, nurture
- [ ] Buyer agreements before showings (NAR settlement); the showing coordinator
- [ ] Listings, the listing assistant, the MLS adapter (RESO Web API) with a fake
- [ ] Offers and transactions, the deadline checklist, broker compliance review; the transaction coordinator
- [ ] Agent commissions on the shared C29 engine

## Phase 4b: Commercial

- [ ] Commercial leases: gross, modified gross and triple net; CAM estimates and annual reconciliation; percentage rent; tenant improvements and allowances
- [ ] Commercial brokerage: LOIs, longer deal stages, landlord and tenant representation

## Phase 5: Integration with StaffSmith

- [ ] One sign-in and one operator console for firms on both products
- [ ] The shared core released on its own schedule
