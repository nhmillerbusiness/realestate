# Questions

Open questions for Nathan, newest at the bottom of each list. When a question is reversible, Claude applies a default and says so ("Default applied"). The ones below wait because they shape the whole build.

## Answered and open

### RE-01: Residential only, or commercial too?

- **Context:** commercial leasing (office, retail, industrial) brings CAM reconciliations, percentage rent and a different brokerage practice.
- **Recommendation:** residential first.
- **Answer (Nathan, Nov 5, 2026):** both residential and commercial.
- **Default applied:** the data model carries commercial lease types (gross, modified gross, triple net) from day one; residential workflows ship first in each module, commercial (CAM reconciliation, percentage rent, tenant improvements, LOIs) follows.
- **Status:** answered

### RE-02: Property management first, brokerage first, or both together?

- **Context:** the concept's build order puts property management first. It's the larger and stickier half: firms rarely switch their system of record.
- **Answer (Nathan, Nov 5, 2026):** both together.
- **Status:** answered

### RE-03: Single-family and small multifamily, or larger apartment communities too?

- **Context:** large communities are where AppFolio, Yardi, Entrata and EliseAI compete hardest.
- **Recommendation:** small portfolios first.
- **Answer (Nathan, Nov 5, 2026):** all of it: single-family, small multifamily and larger communities.
- **Status:** answered

### RE-04: Is there a first firm, as Key Consulting is for StaffSmith?

- **Context:** a design partner sets the defaults, the demo data and the first state.
- **Answer (Nathan, Nov 5, 2026):** not yet, but one is coming.
- **Status:** answered (the demo tenant stands in until then)

### RE-05: Which state first?

- **Context:** trust accounting, security deposits, late fees, notice periods, license law and the MLS are all state-specific.
- **Recommendation:** Arizona.
- **Answer (Nathan, Nov 5, 2026):** Arizona.
- **Status:** answered

### RE-06: The product name

- **Context:** "PropertySmith" is a working name. A trademark and domain check comes first.
- **Answer (Nathan, Nov 5, 2026):** undecided; it depends on finding a domain.
- **Status:** open

### RE-07: When and how to extract the shared core from StaffSmith

- **Context:** the core touches StaffSmith's repo, so it's a StaffSmith decision with its own ADR there.
- **Options:**
  - a separate packages repo;
  - a shared monorepo;
  - published npm packages.
- **Answer (Nathan, Nov 5, 2026):** one common core, with no duplicated fundamentals, in one repo. PropertySmith is built in `staffingplatform/propertysmith/`, on the core in `packages/` (ADR 0001 here; StaffSmith ADR 0023).
- **Status:** answered
