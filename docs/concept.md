# PropertySmith: a real estate platform on the StaffSmith foundation

v0.1 · Nov 5, 2026 · Nathan Miller · committed from the Claude Doc of the same name

PropertySmith (a working name) is a multi-tenant platform for small and mid-sized real estate brokerages and property management firms. It's built on StaffSmith's foundation, with digital workers doing the routine work and people making every consequential decision. Most of the platform's core carries over unchanged; the real estate parts are new modules on the same core.

## The idea in brief

- **Who it serves:**
  - independent brokerages (5 to 100 agents) that also manage rentals;
  - property management firms with roughly 50 to 3,000 units.

  Many small firms do both, and today they run two separate systems: a CRM for sales and a property management system for rentals.
- **What it does:**
  - for the brokerage: leads, nurture, showings, listings, offers, transactions and agent commissions;
  - for property management: owners, properties and units, marketing vacancies, applications and screening, leases, rent, maintenance, inspections, owner statements and trust accounting.
- **Digital workers:** a leasing assistant, a maintenance coordinator, a transaction coordinator and others do the routine work. As in StaffSmith, a person decides anything that affects someone's housing, money or legal position, for example:
  - approving or denying an applicant;
  - a lease or a rent change;
  - an eviction notice;
  - a disbursement;
  - an offer.
- **What it reuses from StaffSmith:**
  - tenancy and row-level security;
  - the AI gateway, the decisions queue and the agent action log;
  - Inbox, tasks and activities;
  - Microsoft 365 sync, texting and calling;
  - templates and writing style;
  - KPIs and workflow rules;
  - custom fields and objects;
  - the integrations hub and the portal;
  - QuickBooks and commissions;
  - the operator console and evals.
- **Why it could win:** the leaders are either strong CRMs with no property management (Follow Up Boss, Lofty, BoldTrail) or strong property management with a light CRM (AppFolio, Buildium). Big operators are adding AI agents fast (AppFolio's Realm-X, EliseAI), but they sell to large portfolios. One agentic platform for the small firm that does both is the gap.
- **Separate from StaffSmith for now:** its own repo and product, sharing the foundation as packages. It's integrated later, when the shared core is extracted (see the build order).

## The market

The market splits three ways, and no product spans all three for a small firm. Prices are as the sources state them; most vendors don't publish prices.

| Segment | Leading products | Who they fit | AI today |
| --- | --- | --- | --- |
| Brokerage CRM and lead generation | [Follow Up Boss](https://www.sierrainteractive.com/insights/blog/best-real-estate-crm/) (about $69 per user a month), Lofty (formerly Chime), BoldTrail (formerly kvCORE), Sierra Interactive (from $299.95 a month), Real Geeks ($399 a month), CINC | Agents, teams and brokerages working buyer and seller leads | Lead follow-up assistants and nurture (Lofty); an AI add-on from $200 a month (CINC) |
| Transaction management | Dotloop, SkySlope, Lone Wolf (from general knowledge; not checked here) | Brokers' compliance review of contracts and documents | Mostly document checks |
| Property management | [AppFolio, Yardi Voyager, Entrata, RealPage, Buildium, DoorLoop](https://www.appfolio.com/blog/best-property-management-softwares-compared-2026) | Buildium and DoorLoop for smaller and single-family portfolios; AppFolio from about 100 to 10,000+ units; Yardi, Entrata and RealPage for large operators | AppFolio's Realm-X Performers for leasing, maintenance, resident messages and accounting |
| AI layer for housing | [EliseAI](https://commercialobserver.com/2026/09/eliseai-ai-agent-apollo/) | Large multifamily operators | Leasing, maintenance and renewals agents; Apollo, one agent across its platform (Sep 2026) |

**What the leaders show about digital workers:**

- **AppFolio** went from a question-and-answer assistant ([Realm-X, Sep 2023](https://www.appfolio.com/newsroom/appfolio-unveils-realm-x-the-property-management-industry-s-first-ever-generative-ai-conversational-interface)) to task agents it calls Performers.
  - In June 2026 it added an accounting Performer, a 24/7 multilingual voice leasing Performer and a [Claude connector](https://rallies.ai/news/appfolio-rolls-out-claude-connector-and-realm-x-ai-tools-lifts-showings-35).
  - It reports 35% more showings booked for early users, and its resident messenger resolving a third of inquiries. These are the vendor's figures.
- **EliseAI** is valued above $1 billion and raised $250 million in August 2025. Its new agent inherits each user's permissions, which is the same rule StaffSmith's MCP server follows.
- **Both sell to large portfolios.** The small brokerage that also manages a few hundred doors runs a CRM plus Buildium or AppFolio, with little AI in either.

**What changed in the rules:** since August 17, 2024, the NAR settlement requires a written buyer agreement before touring, and bans offers of buyer-agent pay in the MLS ([NC Real Estate Commission](https://bulletins.ncrec.gov/has-the-world-exploded-the-nar-settlement-commission-law-and-rules/)). Brokerages need those agreements tracked before every showing, which a transaction assistant can enforce.

## How the foundation maps over

Three products sit on one shared core:

- **Staffing:** StaffSmith today.
- **Brokerage:** a new module.
- **Property management:** a new module.

All three run their digital workers through the AI gateway. Each worker does the routine work; a person makes every consequential decision.

The shared core holds these packages, extracted from StaffSmith:

- tenancy and RLS;
- sign-in and portal;
- AI gateway;
- agent action log;
- decisions queue;
- Inbox and tasks;
- email, texting and calls;
- templates and writing style;
- rules and KPIs;
- custom fields and objects;
- integrations hub;
- finance and commissions.

The Claude Doc draws this as a diagram.

Everything in the core is already built for StaffSmith. PropertySmith adds the two module columns and its own digital workers, and reuses the operator console and evals as they are.

| StaffSmith concept | PropertySmith equivalent |
| --- | --- |
| Company (client) | Owner (property management client) or seller |
| Candidate | Lead, buyer, tenant applicant, resident |
| Job | Listing (for sale) or vacancy (for rent) |
| Submission and stages | Showing, application, offer, each with its stages |
| Placement | Closed transaction, or signed lease |
| Timesheet and invoice | Rent charge, owner statement, management fee |
| Client agreement (C10) | Listing agreement, buyer agreement, management agreement |
| Guarantee (C10) | Tenant placement guarantee (a common property management term) |
| Commissions (C29) | Agent splits, caps and referral fees, the same engine |
| Requirement compliance check (C27h) | Fair Housing wording check on listings, ads and screening criteria |

## Modules

Each module is a feature flag per tenant, as VMS and payroll are in StaffSmith. A brokerage-only firm turns property management off, and the reverse.

### Brokerage: lead to closing

| Area | What it holds | Built on |
| --- | --- | --- |
| Leads | Sources (portals, website, open houses, referrals, sphere), dedupe, routing to agents by rules (area, price, round robin, ponds), speed-to-lead | C14 leads, C21 rules, dedupe |
| Contacts and sphere | Buyers, sellers, past clients, referral partners; relationship dates (home anniversary, birthday); do-not-contact | CRM, C4.1 statuses, C11 custom fields |
| Nurture | Drip and behavioral sequences, saved-search alerts from IDX, market updates | Phase 11 sequences, C6 writing style |
| Buyer agreements | Written agreement before any tour (NAR settlement), its term, compensation and state-required wording; showings are blocked without one | C10 agreements, the decision point |
| Showings | Requests, scheduling with listing agents and sellers, feedback | C13 scheduling |
| Listings | Listing agreements, MLS data (IDX and VOW feeds through a RESO Web API adapter), marketing, seller reports | C15 career site pattern for public pages |
| Offers and transactions | Offers and counters, the accepted contract, a checklist of contingencies and deadlines (inspection, appraisal, financing, closing), documents and e-signature, broker compliance review | C12 tasks, Phase 13 documents, e-signature |
| Agent commissions | Splits, caps, team splits, referral fees, transaction fees, 1099s | C29 commission engine |
| Agent recruiting | Recruiting agents to the brokerage (a staffing problem StaffSmith already solves) | StaffSmith's ATS, reused |

### Property management: owner to resident

| Area | What it holds | Built on |
| --- | --- | --- |
| Owners and agreements | Owners, management agreements (fee percentage, leasing fee, reserves, approval limits), owner portal | Companies, C10 agreements, portal |
| Properties and units | Portfolios, properties, units, amenities, keys, photos, compliance items (smoke detectors, lead-paint disclosure for older homes) | C26 custom objects |
| Marketing and leasing | Vacancy listings syndicated to rental sites, inquiries, tours (self-guided or staffed), applications | C15 public pages, C13 scheduling |
| Screening | Written screening criteria applied the same way to every applicant, consumer reports with FCRA adverse action steps | Phase 9's FCRA flow (Verified First pattern) |
| Leases | Lease generation from state templates, e-signature, renewals, rent changes with notice periods | Phase 8c templates, C10 |
| Rent and resident accounts | Charges, payments, late fees by state rule, deposits, ledgers, resident portal | Portal, payments adapter |
| Maintenance | Requests with photos, triage and emergency rules, vendor dispatch, owner approval over the limit, completion and billing | C12 tasks, C21 rules |
| Inspections | Move-in, move-out and periodic inspections on the phone, with photos | C22 mobile app |
| Accounting | Trust accounting per state, bank reconciliation, owner statements and disbursements, management fees, 1099s, a QuickBooks export or the firm's own ledger | C16 QuickBooks pattern, plus a trust ledger (new) |

## Digital workers

Each digital worker:

- is an agent on the AI gateway;
- is logged in the agent action log;
- has the permissions of the person or role it works for, the rule EliseAI's Apollo and StaffSmith's MCP server already follow.

Anything in the last column goes to the decisions queue and waits for a named person.

| Digital worker | What it does | A person decides |
| --- | --- | --- |
| Lead concierge (brokerage) | Answers new leads within minutes by text, email or voice, qualifies (timeline, area, price, financing), books a call or showing, routes to the right agent | Which agent takes a lead when the rules don't settle it; any price or legal advice |
| Nurture writer | Drafts drips, market updates and saved-search notes in the agent's own voice | Sending to a new list; anything with a claim about a home or a neighborhood |
| Showing coordinator | Checks the buyer agreement, books showings with listing agents, collects feedback | Showing without a signed buyer agreement is blocked, not decided |
| Listing assistant | Drafts listing copy from photos and the agent's notes, runs the Fair Housing wording check, prepares the seller's weekly report | Publishing the listing; the price |
| Transaction coordinator | Builds the deadline checklist from the contract, chases documents and signatures, flags a missed contingency date | Waiving a contingency, extending a deadline, broker compliance approval |
| Leasing assistant (PM) | Answers rental inquiries around the clock, books tours, sends the application, explains the written screening criteria | Approving or denying an applicant, and the terms offered |
| Screening reviewer | Assembles the application file against the firm's written criteria; prepares the adverse action notice if a person denies | Approve, deny, or approve with conditions (FCRA adverse action follows a person's decision) |
| Maintenance coordinator | Triages requests from photos and text, spots emergencies, dispatches vendors within the owner's approval limit, follows up, bills | Work over the owner's limit; anything that charges a resident |
| Renewals and rent assistant | Proposes renewal terms from the market and the lease, sends notices on the state's schedule, reminds residents of rent | Every rent change, late fee waiver, payment plan, and any eviction notice |
| Accounting assistant | Codes invoices, matches bank lines, drafts owner statements and disbursements, flags trust account mismatches | Every disbursement from the trust account; month-end close |
| Owner relations assistant | Answers owners' questions from their statements and work orders; drafts the monthly owner update | Changes to the management agreement |
| Inspection assistant | Builds the inspection report from photos and notes on the phone; compares move-in to move-out | Deposit deductions |

**Autonomy settings** follow StaffSmith's pattern, set by tenant and by worker. A worker can draft only, act with review, or act within limits (for example a dollar limit for vendors, or quiet hours for messages). The decisions in the last column can't be set to act alone.

## Compliance guardrails

Fair Housing is to PropertySmith what AI-in-hiring rules are to StaffSmith: the controls are built in, not bolted on.

The summaries below are for design, not legal advice. Counsel confirms each before launch, and legal wording stays a marked placeholder until then (the StaffSmith rule).

| Rule | What it means for the platform | How PropertySmith enforces it |
| --- | --- | --- |
| Fair Housing Act, plus state and local protected classes (often source of income) | No steering, no discriminatory ads or screening, reasonable accommodations handled by a person. HUD withdrew its 2024 guidance on digital advertising, effective Sep 17, 2025 ([Orrick](https://infobytes.orrick.com/2026-04-10/hud-withdraws-eight-fair-housing-guidance-documents-as-part-of-deregulatory-review/)), but that was guidance; the Act itself still applies | A Fair Housing wording check on listings, ads, messages and screening criteria (the C27h pattern); agents never describe neighborhoods by who lives there; accommodation requests always go to a person; ad audiences never targeted by protected class |
| FCRA (tenant screening) | Consumer reports only with permission; adverse action notices when a report affects a denial | Phase 9's FCRA flow: a person decides, the notice follows, wording is counsel-approved |
| Written, consistent screening criteria | The same criteria for every applicant, published before applying | Criteria versioned per property; the screening reviewer only checks against them; overrides need a reason and are reported |
| NAR settlement (since Aug 17, 2024) | A written buyer agreement before touring; no offers of buyer-agent pay in the MLS | Showings blocked without an agreement on file; compensation kept out of MLS feeds |
| RESPA Section 8 | No kickbacks or unearned referral fees in settlement services; affiliated business disclosures | Referral fees only to licensees, flagged for broker review; affiliated-business disclosure templates |
| State license law | Unlicensed assistants can't do licensed activities (in most states: negotiating, interpreting contracts, showing on their own) | Digital workers schedule, inform and draft; they never negotiate, advise on price or terms, or interpret a contract. The line per state is a counsel question |
| Trust accounting (state rules) | Client and resident money held separately from the firm's, reconciled on the state's schedule | A trust ledger per bank account; reconciliation the accounting assistant prepares and a person signs; no disbursement without a person |
| Security deposits and late fees (state rules) | Limits, holding rules, return deadlines, itemized deductions | Rules per state in configuration; deadline tasks; deductions decided by a person |
| Lead-based paint disclosure | Federal disclosure for housing built before 1978 | A property attribute that adds the disclosure to listings and leases |
| TCPA and state texting rules | Consent before marketing texts and calls; quiet hours | StaffSmith's SMS opt-in and quiet hours, unchanged |
| MLS and IDX rules | Display and attribution rules per MLS | The MLS adapter carries each MLS's display settings |

**The eval gates carry over too.** Before a prompt version is promoted:

- paired applicants who differ only by a protected trait must get the same screening result;
- the Fair Housing check must catch the phrases in its test set.

## Integrations, pricing and build order

### Integrations (all behind adapters with fakes, in the StaffSmith v0.9.9 hub)

| Category | What connects | Notes |
| --- | --- | --- |
| MLS | RESO Web API feeds for listings, IDX display | Each MLS licenses access separately; the firm's membership is required |
| Listing and rental syndication | Rental listing sites, portals | Through a syndication partner, as StaffSmith's job distribution |
| Lead sources | Portal leads, website forms, open-house sign-ins | Email parsing and webhooks |
| Tenant screening | A screening bureau with FCRA flows | Same pattern as Verified First |
| Payments | Rent by ACH and card, owner disbursements | A payments provider; trust account rules decide where money lands |
| Accounting | QuickBooks Online (management company books), the trust ledger in PropertySmith | The C16 adapter, extended |
| E-signature, email, calendar, texting, calling | Adobe Acrobat Sign or DocuSign; Microsoft 365; the SMS and calling adapters | Reused as they are |
| Access and devices | Smart locks and lockboxes for self-guided tours | Later; vendor choice open |

### Pricing ideas (to decide)

Property management software is usually priced per unit (door) per month, and brokerage CRMs per agent seat. The sources above publish few numbers. PropertySmith could offer:

- **Seats and doors:** per agent seat for brokerage, per door for property management.
- **Outcome-based digital workers:** StaffSmith's commissions-only idea, mapped to real estate milestones:
  - a share of a closed transaction's side where the lead concierge produced the client;
  - or a flat fee per lease the leasing assistant filled.

  It waits on the same conversation with China, and the same conflict-of-interest guardrails apply.

### Build order

1. **Extract the shared core** from StaffSmith into packages:
   - tenancy, gateway, decisions and the action log;
   - Inbox and tasks, comms, templates and rules;
   - custom objects, the integrations hub, the portal and the operator console.

   StaffSmith keeps running on them unchanged.
2. **PropertySmith skeleton:** its own repo and AWS accounts (the same Lambda, Aurora and SQS defaults), and its own demo tenant.
3. **Property management first:** owners, properties, units, leasing, applications and screening, leases. It's the larger and stickier half: firms rarely switch their system of record.
4. **Rent, maintenance and trust accounting,** with the maintenance coordinator and accounting assistant.
5. **Brokerage:** leads, nurture, buyer agreements, showings, transactions, agent commissions.
6. **MLS and syndication adapters** per market, starting with Arizona's.
7. **Integration with StaffSmith:** one sign-in and one operator console for firms that use both, and the shared core released on its own schedule.

## Open questions for Nathan

See `docs/QUESTIONS.md` (RE-01 to RE-07).

## Sources

- [Best Real Estate CRMs in 2026: An Honest Comparison](https://www.sierrainteractive.com/insights/blog/best-real-estate-crm/), Sierra Interactive, Sep 25, 2026 (a vendor's comparison)
- [Best property management software compared, 2026](https://www.appfolio.com/blog/best-property-management-softwares-compared-2026), AppFolio, Oct 15, 2026 (a vendor's comparison)
- [AppFolio unveils Realm-X](https://www.appfolio.com/newsroom/appfolio-unveils-realm-x-the-property-management-industry-s-first-ever-generative-ai-conversational-interface), AppFolio, Sep 21, 2023
- [AppFolio rolls out Claude connector and Realm-X AI tools](https://rallies.ai/news/appfolio-rolls-out-claude-connector-and-realm-x-ai-tools-lifts-showings-35), Jun 16, 2026
- [EliseAI launches AI agent Apollo](https://commercialobserver.com/2026/09/eliseai-ai-agent-apollo/), Commercial Observer, Sep 3, 2026
- [Has the world exploded? The NAR settlement, commission law and rules](https://bulletins.ncrec.gov/has-the-world-exploded-the-nar-settlement-commission-law-and-rules/), North Carolina Real Estate Commission
- [HUD withdraws eight fair housing guidance documents](https://infobytes.orrick.com/2026-04-10/hud-withdraws-eight-fair-housing-guidance-documents-as-part-of-deregulatory-review/), Orrick, Apr 10, 2026

Transaction management products, per-door pricing and the state rules summarized above are from general knowledge and weren't checked against sources here.
