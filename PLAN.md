# PLAN — ewing-research-landscape

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

An open, linked, citable **map of the Ewing Sarcoma research ecosystem** — the organizations
(funders, research institutions, advocacy foundations, consortia), the research efforts and
registered studies, and the grants/awards that fund them — built **only** from open-access,
aggregate, organization- and award-level public records, with **provenance on every assertion**.
This is a transparency and orientation tool, **not** a clinical, genomic, or patient-data project.

> **For families facing Ewing Sarcoma.** Ewing Sarcoma is a rare, aggressive bone/soft-tissue
> cancer that most often strikes children, teens, and young adults. Families who receive this
> diagnosis are thrown into an unfamiliar world and often ask, quietly and urgently, *"Who is
> actually working on this? Where is the money going? Is anyone trying to help my child?"* Today
> there is no single honest answer. This project exists to give families, advocates, and
> researchers a clear, sourced map of who is working on Ewing and where the gaps are — so the
> effort is **legible** to the people it is meant to serve. It will **never** give medical advice,
> rank treatments, or tell anyone what to do for a patient. We hold that line with care.

## Executive summary

There is no open, queryable, source-linked map of the Ewing Sarcoma research landscape. The
information exists — in NIH RePORTER, the EU's CORDIS, UKRI's Gateway to Research, the trial
registries, OpenAlex, ROR, and the public filings of dozens of small Ewing/sarcoma foundations —
but it is **scattered across a dozen systems, in incompatible formats, with no shared identifiers,
and no provenance a family or advocate could check.** The richest *integrated* views of this
landscape (Dimensions, Web of Science, Scopus, Candid/Foundation Directory) are **proprietary
research-intelligence products behind license terms that forbid redistribution** — exactly the
people who most need the picture (families, patient advocates, small foundations, early-career
researchers) cannot get it.

This project builds an **openly-licensed dataset + lightweight explorer** of the Ewing research
ecosystem from open sources only, where **every assertion carries a resolvable citation** to a
specific public record, and entities are reconciled to **canonical persistent identifiers** (ROR
for organizations, ORCID for people, Crossref Funder Registry for funders, NCT numbers for trials,
DOIs for outputs) so the map is interoperable and reconcilable against the wider open-data web from
day one. Crucially, it publishes a **"known gaps" ledger** — an honest account of what is *not*
covered — because a transparency tool that hides its own blind spots is worse than none.

The single most important constraint is **data scope and licensing** (see
[Data, licensing & compliance](#data-licensing--compliance)). Under Elyos's binding cancer
guardrails, this project works **only with open-access, aggregate, organization-/award-level
metadata**. It touches **no patient data of any kind** — no controlled-access genomics (dbGaP,
EGA), no individual-level biobank or clinical records, no identifiable patient information. The
project's privacy surface is limited to **public professional facts about named investigators**
(from public grant and registry records), handled conservatively with a correction/removal process.
Scraping or re-publishing proprietary research-intelligence databases is **out of scope and never
acceptable.**

Risk tier: **low** overall — driven by source-license compliance and living-investigator data
hygiene, both of which are well-bounded. The one place risk rises is any **family/advocate-facing
explanatory text**: that is kept strictly navigational and non-clinical, carries a standing "not
medical advice" notice, and is patient-advocate reviewed. Any content that crosses into clinical
interpretation of a trial or treatment is **out of scope here** and belongs to the sibling
`high`-risk projects (`ewing-trial-finder`, `ewing-family-guide`) behind oncologist + advocate
sign-off.

## Problem & beneficiaries

**The problem.** Ewing Sarcoma is rare (roughly 1 in a million people per year; ~200 new U.S.
diagnoses annually), which means research is fragmented across many small efforts in many
countries, funded by a long tail of government agencies, large charities, and tiny
family-founded foundations. There is no consolidated, open, machine-readable view of:
- **who funds Ewing research** (and how much, through what mechanism, over what years),
- **who does it** (institutions, labs, consortia, principal investigators),
- **what efforts and registered studies exist** (as aggregate, public records — not patient data),
- **how these connect** (this funder → this institution → this program → these public outputs),
- and **where the gaps are** (under-funded subtopics, under-served regions, stalled efforts).

The integrated commercial tools that *could* answer these questions are paywalled and forbid
redistribution; the open public records that *could* feed an honest answer are un-linked,
inconsistently identified, and hard to query at scale.

**Beneficiaries.**
- **Families and caregivers** facing an Ewing diagnosis who want to understand — without a
  paywall and without being given medical advice — that real, organized effort exists and where it
  is happening. Orientation, not treatment guidance.
- **Patient advocates and small Ewing/sarcoma foundations** who need to see the funding landscape
  to decide where their limited dollars add the most, avoid duplication, and find collaborators.
- **Researchers** (especially early-career and those entering the field) mapping who works on what,
  who funds it, and where the white space is.
- **Funders and grant-makers** wanting an honest, independent view of coverage and gaps.
- **Journalists, policy analysts, and the public** holding the research ecosystem to account.
- **Downstream open projects** — the sibling Ewing projects (`ewing-open-data-catalog`,
  `ewsr1-fli1-knowledge-graph`, `ewing-trial-finder`) and the wider open-science graph
  (OpenAlex, ROR, Wikidata) that can reconcile against and reuse this map.

**Verified need.** The *gap* (no open, source-linked map of the Ewing research ecosystem exists,
and the integrated alternatives are paywalled) is real and demonstrable. However, a **named partner
organization or steward who will adopt, host, cite, and keep the map alive is TO BE SECURED.** The
honest reading: the need is genuine, but the last-mile beneficiary (a sarcoma advocacy foundation,
a research consortium, a university library/digital-science team, or a rare-cancer alliance) has
not yet signed on. Per the Elyos quality bar ("delivered, not merged"), securing this partner is a
first-class M0/M4 objective and a precondition for declaring the project *shipped*. All tasks ship
with `verifiedNeed: false` until a committed partner exists.

**Partner org.** TO BE SECURED. Candidate stewards: a Ewing/sarcoma advocacy foundation, a
pediatric-oncology research consortium, a rare-cancer alliance, an academic open-science /
digital-humanities center, or a research-funder transparency initiative.

## Goals and non-goals

**Goals**
- Publish an openly-licensed, queryable map of the Ewing research ecosystem (organizations,
  efforts, grants/awards, registered studies as aggregate records, and public outputs) with
  **provenance on every assertion**.
- Use **only** open-access, aggregate, organization-/award-level public records (no patient data).
- Reconcile every entity to **canonical persistent identifiers** (ROR, ORCID, Crossref Funder
  Registry, NCT, DOI) rather than minting new IDs where an authority exists.
- Define a reproducible, **published Ewing inclusion query** so "what counts as Ewing research" is
  transparent and auditable, not a black box.
- Publish a **"known gaps" / coverage ledger** that states honestly what is and is not covered.
- Provide standard open exports (CSV + JSON-LD) and a simple, no-account public explorer.
- Handle **multi-currency grant amounts** honestly (retain original; normalize with dated FX).
- Secure at least one advocacy/research **steward** that adopts and cites the map.
- Treat any family/advocate-facing text as **non-clinical orientation only**, advocate-reviewed,
  with a standing "not medical advice" notice.

**Non-goals**
- **Not** a patient-data project. No controlled-access genomics (dbGaP/EGA), no individual-level
  biobank/clinical/registry records, no identifiable patient information — ever.
- **Not** medical advice. It does **not** rank, recommend, or interpret treatments or trials for
  any patient, and does not tell families what to do. (Clinical/plain-language trial explanation
  lives in the sibling `high`-risk projects, behind oncologist + advocate review.)
- **Not** a scrape or mirror of Dimensions, Web of Science, Scopus, Candid/Foundation Directory,
  or any other proprietary research-intelligence database.
- **Not** a ranking or "scorecard" of organizations, researchers, or funders. It maps and links;
  it does not adjudicate who is "best."
- **Not** a dossier on individuals. It records only public professional facts (role, affiliation,
  public award/registry record) and supports correction/removal.
- **Not** original scientific claims. It structures what public funding/registry/output records
  attest; gaps stay gaps and are logged, not filled by inference.
- **Not** a hosted commercial product, account system, or for-profit data package.

## Success metrics (outcomes)

Outcome-based, beneficiary-centric. Baselines are zero at project start unless noted.

| Metric | Baseline | Target (first 12 months) |
| --- | --- | --- |
| Organizations cataloged with ≥1 cited open source | 0 | ≥ 300 (funders, institutions, foundations, consortia) |
| Grants/awards recorded with full provenance | 0 | ≥ 1,500 award records (Ewing-relevant) |
| Registered-study records linked as **aggregate** public records (NCT-identified) | 0 | ≥ 150 |
| Share of published assertions carrying a resolvable provenance link | n/a | **100%** (hard gate; un-sourced assertions are not published) |
| Organizations reconciled to a ROR ID | 0 | ≥ 85% of institutions/funders |
| Funders reconciled to a Crossref Funder Registry ID | 0 | ≥ 80% of funders |
| Grant records retaining **original currency + amount** alongside any normalized value | n/a | **100%** (no original figure is ever discarded) |
| Distinct open source systems integrated | 0 | ≥ 4 (e.g. NIH RePORTER + CORDIS + Gateway to Research + AACT/ClinicalTrials.gov) |
| Data-freshness: snapshot date recorded on every record; refreshed sources ≤ 90 days old | n/a | 100% timestamped; ≥ 90% within 90 days after M4 |
| Accuracy: stratified audit sample verifying against the cited source | n/a | ≥ 95% verified (see sampling frame below) |
| Coverage honesty: a published "known gaps" ledger updated each release | none | present and current every release |
| Steward/partner adopting or citing the map | 0 | ≥ 1 committed steward; ≥ 1 documented citation/use |
| Patient-advocate review of any family-facing text | none | 100% of family/advocate-facing text advocate-reviewed before publish |
| Reuse: external downloads / queries of exports | 0 | tracked from M3; growth trend reported quarterly |

**Accuracy-audit sampling frame (pins the accuracy metric).** The ≥95% target is meaningless
without a defined sample, so each release audit uses: a **minimum sample size of 200 assertions**
(or the whole release if smaller); **stratified sampling** across strata defined by *source system*
and by *assertion type* (organization identity, grant amount/date, funder→recipient link,
study-record linkage, output linkage), so no source or field type escapes review; and an **auditor
independent of the extractor** of the sampled records (no self-grading). Grant **amount** and
**currency** assertions are a mandatory stratum because a wrong figure is the most damaging error a
transparency tool can make.

We explicitly **do not** treat raw record count, PRs merged, or commits as success. A large map
with weak provenance, stale figures, or a hidden gaps profile is a **failure** under this plan.

## Scope

**In scope**
- Data model/ontology and a source allow-list (with per-source license determination recorded).
- A reproducible, published **Ewing inclusion-query** definition (how records are selected).
- Structured extraction of **organizations, research efforts, grants/awards, registered-study
  records (aggregate), public outputs, and their relationships** from open sources.
- Reconciliation to ROR / ORCID / Crossref Funder Registry / NCT / DOI; cross-source dedup with
  human-confirmed merges.
- Provenance, license, and snapshot-date metadata on every node and assertion.
- Multi-currency amount handling (original retained; dated-FX normalization recorded).
- CSV + JSON-LD exports and a simple, no-account public explorer.
- A published **"known gaps" / coverage ledger**.
- A **non-clinical** family/advocate orientation layer (advocate-reviewed; "not medical advice").
- Outreach for an adopting steward and for domain/advocate reviewers.

**Out of scope (explicit)**
- **Any patient-level or controlled-access data** — dbGaP, EGA, individual-level biobank/clinical/
  registry/genomic data, or any identifiable patient information. This is a **hard refusal** under
  Elyos cancer guardrails, not a deprioritized item.
- **Any scraping, bulk download, API harvesting, or re-publication of Dimensions, Web of Science,
  Scopus, Candid/Foundation Directory Online, or any other proprietary research-intelligence
  database.** Hard refusal.
- **Medical advice or clinical interpretation** — ranking/recommending/explaining treatments or
  trials for a patient. (Belongs to the gated `high`-risk sibling projects.)
- **Ranking or scoring** organizations, researchers, or funders ("best lab," "top funder").
- **Dossiers on individuals** or any non-public personal data (home address, personal contact,
  health, family). Only public professional facts.
- **Inferred/AI-generated "fill-in"** of unknown funding, links, or outcomes. Gaps stay gaps and
  are logged in the gaps ledger.
- Paid features, user accounts, or for-profit packaging of the data.

## Solution approach & architecture

A **data/content pipeline** project (with supporting TypeScript tooling), not a hosted service.

**Pipeline stages**
1. **Source intake & licensing gate** — every candidate source is logged in a machine-readable
   `sources/allowlist.yml` with: name, custodian, URL/API, format, license (and license URL),
   redistribution terms, attribution requirement, refresh cadence, and an explicit
   `status: approved | rejected | pending`. **Nothing is processed until `approved`.** Proprietary
   research-intelligence databases are pre-listed as `rejected` (categorical).
2. **Ewing scope definition** — a published, version-controlled **inclusion query** (MeSH/keyword
   terms such as *Ewing sarcoma*, *EWSR1*, *FLI1/ETS fusion family*, *Askin tumor / PNET* where
   appropriate, plus an expert-curated seed list of known Ewing/sarcoma orgs and consortia). The
   query is recorded so selection is reproducible and auditable; over-inclusion vs. precision
   trade-offs are documented and a domain reviewer validates the seed.
3. **Extraction** — per-source extractors turn open records (a NIH RePORTER result set, a CORDIS
   project export, an AACT trial record) into typed entities. Extraction is **deterministic and
   assistive**: it maps fields from authoritative records; it does **not** infer unknown values.
   Ambiguous fields are flagged for human review, never guessed.
4. **Normalization & provenance binding** — records are mapped to ontology entities; **every
   assertion is wrapped with a provenance statement** (source record IRI/URL + license + retrieval
   snapshot date + extraction method + confidence). Grant amounts are normalized to a common
   currency using a **dated FX rate**, while the **original currency and amount are always
   retained**; the FX source and date are themselves provenanced.
5. **Reconciliation & dedup** — entities are matched to canonical IDs (ROR, ORCID, Crossref Funder
   Registry, NCT, DOI) and against within-graph duplicates. Matching uses an explicit **blocking-key
   strategy** (e.g., normalized org name + country + ROR candidate) and is tuned for **precision
   over recall**; proposed merges are **human-confirmed**, reversible, and retain both records'
   provenance. The bar is **zero confirmed false merges** in the audit sample.
6. **Validation** — schema (SHACL/JSON-Schema) validation + a provenance-completeness linter +
   an allow-list gate (no record from a non-`approved` source) + a freshness check (every record
   carries a snapshot date), all enforced in CI.
7. **Publish** — versioned CSV + JSON-LD dumps, a simple static explorer, a data dictionary, and
   the **"known gaps" ledger**, under the persistent-identifier namespace.

**Tech stack**
- Tooling/extractors/validators: **TypeScript, ESM, pnpm** (per Elyos conventions).
- Serialization: **CSV** (human-friendly) + **JSON-LD** (linked, with dereferenceable IRIs).
- Validation: **JSON-Schema + SHACL** shapes + a custom provenance/freshness linter in CI.
- Reconciliation: **ROR API**, **Crossref Funder Registry**, **ORCID**, **OpenAlex** (CC0)
  reconciliation clients; human review via a lightweight worklist.
- Explorer: a **static-site** explorer over the JSON-LD — no accounts, no visitor PII, links to
  raw exports and to each assertion's source.

**Data model (core entities)**
- **Organization** — funder, research institution, advocacy/foundation, consortium, or
  (non-commercial-context) company; aligned to `schema:Organization` / ROR.
- **Person** — investigator/PI as a **public professional role only**; aligned to ORCID where
  available. Minimal fields (name, affiliation, role, public IDs); no personal/contact/health data.
- **Grant / Award** — a funding award (funder → recipient org, mechanism, amount + currency,
  start/end dates, public award ID); the FX-normalized amount is an *additional*, provenanced field.
- **ResearchEffort** — a program/project/consortium initiative; the composite node that ties
  grants, people, organizations, and outputs together. (The only entity type for which we mint our
  own IDs — see key decisions.)
- **StudyRecord** — a **registered study as an aggregate public record** (NCT-identified), holding
  only registry-level metadata. **No participant/patient data.**
- **Output** — a public research output (publication/dataset) as evidence of effort; aligned to
  DOI / OpenAlex work ID. Metadata only.
- **FundingSource / Source** — the open record a claim came from (license + snapshot date).
- **Place** — aligned to `schema:Place` / Wikidata.

**Relationships:** `funds` (Grant), `conducts`/`affiliatedWith`, `partOf` (consortium),
`investigates` (Person↔Effort), `registeredAs` (Effort↔StudyRecord), `outputOf` (Output↔Effort),
`locatedIn`.

**Key decisions (to ratify in M0)**
- **Reuse canonical IDs; mint sparingly.** Organizations → **ROR**, people → **ORCID**, funders →
  **Crossref Funder Registry**, studies → **NCT**, outputs → **DOI/OpenAlex**. We mint our own
  persistent IDs **only** for the composite `ResearchEffort` node, under a host-independent
  persistent identifier (w3id.org/PURL), decoupled from the unsecured steward.
- **Provenance mechanism & assertion unit.** Pick one mechanism (named graphs + PROV-O leaning,
  RDF-star evaluated) and apply uniformly; the choice **defines the countable "assertion"** the
  100%-provenance CI gate measures.
- **Currency normalization policy.** Original currency + amount are canonical and never discarded;
  a normalized value is an additional field carrying its FX rate, FX source, and FX date as
  provenance. No silent currency conversion.
- **Snapshot/freshness model.** Every record carries a `retrievedAt` date and the source's stated
  "last updated" where available; staleness is computed and surfaced, never hidden.
- **No-ranking rule.** The schema deliberately has **no** quality/ranking field; the explorer
  sorts and filters but never scores entities.

## Data, licensing & compliance

**This is the headline gate for the project. Read this section before doing any data work.**

### Hard boundary 1 — cancer guardrails: open/aggregate/org-level data only, no patient data
Under Elyos's **binding cancer guardrails**, this project works **only with open-access, aggregate,
organization- and award-level metadata**. The following are **OUT OF SCOPE and never acceptable**,
with no "we'll be careful" exception:
- **Controlled-access data** — dbGaP, EGA, or any access-restricted genomic/clinical repository.
- **Individual-level biobank, clinical, or registry data**, or **any identifiable patient
  information** whatsoever.
- Patient-level genomics, samples, images, or outcomes.

By construction this project consumes only **funding records, organization registries, and
aggregate registered-study metadata** — it has **no reason to touch patient data**, and the
allow-list gate exists partly to guarantee it never drifts into doing so. Registered studies are
recorded **only** at the registry-record level (title, sponsor, phase, status, NCT ID, public
summary) — these are public aggregate facts, not participant data.

### Hard boundary 2 — proprietary research-intelligence databases are out of scope
A map **scraped, harvested, or bulk-copied from Dimensions, Web of Science, Scopus,
Candid/Foundation Directory Online, or any comparable proprietary product** would **violate their
license terms and the copyright in their compiled databases**, and is therefore **OUT OF SCOPE and
never acceptable.** This covers automated scraping/crawling/API-harvesting, re-publishing their
records or compiled structure, and laundering such data through an intermediary export. We assume
both database-copyright and ToS protections apply and **do not touch these systems** absent an
explicit written agreement.

**Closing the data-laundering hole.** A contributor could copy a proprietary record and back-fill a
plausible open citation. Three controls make that detectable and unacceptable:
- **Record-level citations are required** — a citation must resolve to the specific open record
  consulted (a RePORTER project URL, a CORDIS project ID, an AACT/NCT record), never to a database
  "as a whole." Collection-level citations are rejected at review.
- **Contributor attestation of open sourcing** — each contributed batch carries a signed
  attestation that the facts were read from the cited open source directly, not derived from a
  proprietary research-intelligence product.
- **Spot-checks for proprietary-distinctive fields** — reviewers sample for tell-tale artifacts of
  the proprietary compilations (their derived metrics, normalized identifiers, or arrangement) that
  would not appear in the raw open record; a hit triggers rejection and a flag.

### Approved sources (open-access / openly-licensed only)
Every source must be entered in `sources/allowlist.yml` with a recorded license basis and an
`approved` status before use. Candidate approved sources and their licenses **as recorded at intake
(verify each at use time — licenses change):**
- **NIH RePORTER / NIH ExPORTER** (U.S. federal grant data) — U.S. government work → **public
  domain** (verify the specific export's terms).
- **EU CORDIS** (EU-funded research projects) — **CC BY 4.0** (attribution required).
- **UKRI Gateway to Research** — **Open Government Licence (OGL) v3.0** (attribution required).
- **ClinicalTrials.gov / AACT** — ClinicalTrials.gov records are U.S. government **public domain**;
  the cleaner intake is the **AACT** database (CTTI), which provides bulk, well-described data.
  Respect the registry's **terms of use / acceptable-use** (no implication of endorsement; follow
  API terms). Record only **aggregate registry-level** fields.
- **ROR** (Research Organization Registry) — **CC0**.
- **Crossref Funder Registry** — **CC0**.
- **OpenAlex** — **CC0** (works/authorships metadata for output linking).
- **ORCID** public records — used under ORCID's public-data terms; store only public professional
  identifiers/affiliations the researcher has made public.
- **IRS Form 990 / ProPublica Nonprofit Explorer** (U.S. nonprofit foundation filings) — public
  records; verify the specific access channel's terms.
- **Wikidata** (CC0) / **Wikipedia** (CC BY-SA 4.0) — for reconciliation and linking; prefer
  Wikidata (CC0); any Wikipedia-derived **text** triggers CC BY-SA share-alike attribution.

**Caveats we will not gloss over:** an "open" record can be wrapped by a provider's restrictive API
terms or a copyrighted presentation; "open" must be verified for the *specific access channel and
fields* used, not assumed. Each allow-list entry records this analysis and the attribution string
that must be surfaced.

### Provenance model
- **Every assertion** links to its source record at **record-level granularity** (not the database)
  and records the source's license, the **retrieval snapshot date**, the extraction method, and a
  confidence value.
- **Grant amounts** additionally record original currency + amount (canonical) and, if normalized,
  the FX rate/source/date.
- Un-sourced assertions are **never published** — enforced as a CI gate over the countable
  assertion unit fixed by the provenance-mechanism decision.
- Conflicting source values are retained side by side with their respective provenance; the map
  does not silently pick a winner.

### Privacy / PII stance
- The project's **only** personal-data surface is **public professional facts about named
  investigators** drawn from public grant/registry/ORCID records: name, professional affiliation,
  role on a public award, public identifiers (ORCID). **No** personal/contact/home/health/family
  data; **no** non-public data.
- **No patient data of any kind** (see Hard boundary 1).
- A documented **correction & removal process**: a named individual may request correction or
  removal of their professional record; requests are honored absent an overriding public-interest
  reason, and the source link makes every claim auditable.
- No collection of visitor/contributor PII beyond standard open-source attribution a contributor
  chooses to provide. The explorer sets no tracking that profiles visitors.

### Attribution & output license
- **Code:** **MIT**. **Data/content:** **CC BY 4.0** (because CORDIS CC BY and UKRI OGL components
  carry attribution obligations that propagate; CC BY satisfies them cleanly across the mixed
  corpus). Components derived purely from CC0/PD sources are labeled as such; any **CC BY-SA**
  (Wikipedia text) material, if used, is segregated and its share-alike obligation honored.
- Per-source required attributions (CORDIS, UKRI/OGL, Wikipedia, ROR/Crossref/OpenAlex
  acknowledgements) are recorded in the allow-list and surfaced in the dataset and explorer.

### Family/advocate-facing content
Any text aimed at families/advocates is **non-clinical orientation only** (e.g., "this foundation
funds Ewing research; here is its public record"), carries a standing **"This is not medical advice"**
notice, links to its sources, and is **patient-advocate reviewed** before publish. Anything that
would interpret a treatment or trial for a patient is **out of scope** and redirected to the
`high`-risk sibling projects under oncologist + advocate sign-off.

## Quality, review & risk gates

**Risk tier: low** overall, with three review dimensions; the first two are required before any
deed is "done," the third applies to any family/advocate-facing text.

1. **Source-license review (primary gate).** Before any source is processed, a reviewer confirms the
   `sources/allowlist.yml` entry: source is open/openly-licensed, the *specific access channel and
   fields* are cleared, attribution obligations are recorded, and it is **not** a proprietary
   research-intelligence product and **not** patient data. No extraction may start against a
   `pending`/`rejected` source. Any task proposing to touch a proprietary system **or any
   patient-level/controlled-access data** is **refused and flagged** per Elyos guardrails.
2. **Accuracy / citation review.** A reviewer samples extracted assertions against their cited open
   records (stratified frame above); mis-citations, wrong amounts/currencies/dates, false
   funder→recipient links, or invented values block sign-off. Conflicting values must be retained,
   not flattened.
3. **Patient-advocate review (family-facing text only).** Any family/advocate-facing text is
   reviewed by a patient advocate for tone, accuracy, the "not medical advice" framing, and that it
   stays strictly non-clinical. If clinical content has crept in, it is removed and the task is
   redirected to a sibling `high`-risk project.

**Definition of Shipped (project level).** A published, openly-licensed, queryable map of the Ewing
research ecosystem with: **100%** provenance on assertions; ≥4 integrated open sources; canonical-ID
reconciliation at target coverage; original currency/amount retained on 100% of grants; a current
**"known gaps" ledger**; passing CI (schema + provenance + allow-list + freshness); **at least one
advocacy/research steward that has adopted or cited it**; and any family-facing text
advocate-reviewed. Per Elyos, *delivered ≠ merged* — the map must be in a beneficiary's hands.

**Per-deed Definition of Done.** Acceptance criteria met + CI green (schema/provenance/allow-list/
freshness) + source-license review passed + accuracy/citation review passed + (if family-facing)
advocate review passed + output published under the declared license.

## Roadmap & milestones

**M0 — Foundation, scope & compliance spine (cold-start).**
Goal: establish the rails so no data work can bypass the license/provenance/scope gates.
Exit criteria: (a) data model v0 published covering the core entities, mapped to schema.org /
ROR / Crossref / NCT / DOI; (b) `sources/allowlist.yml` schema defined with ≥3 sources analyzed and
≥1 `approved`, and proprietary products + patient-data categorically `rejected`; (c) provenance
mechanism ratified **including the countable assertion unit**, plus the **currency-normalization**
and **snapshot/freshness** policies; (d) the **persistent-ID reuse policy** committed (ROR/ORCID/
Funder Registry/NCT/DOI; mint only `ResearchEffort` IDs under a w3id.org/PURL namespace);
(e) the **living-investigator data + correction/removal policy** published; (f) the **published
Ewing inclusion-query** drafted and validated by a domain reviewer; (g) CI provenance + schema +
allow-list + freshness gates scaffolded; (h) a **qualified source-license reviewer named** (hard
exit; documented fallback if the seat is empty — M0 cannot exit and escalation begins); (i) steward
+ domain/advocate-reviewer outreach started (status logged).

**M1 — First sourced slice (proof of pipeline).**
Goal: end-to-end one source (NIH RePORTER, Ewing-filtered) into the map with full provenance and ROR
reconciliation.
**Hard entry precondition:** the NIH RePORTER access path and its public-domain terms are recorded
`approved` in the allow-list, and the Ewing inclusion-query is published, before extraction starts.
Exit criteria: (a) Ewing-relevant NIH awards extracted into Organization/Grant/Person/ResearchEffort
records; (b) **100%** of new assertions carry provenance + snapshot date and pass CI; (c) ≥85% of
institutions/funders reconciled to ROR; (d) **100%** of grants retain original currency/amount;
(e) stratified accuracy audit (≥200, independent auditor) ≥95% verified; (f) CSV + JSON-LD export
produced under the persistent-ID namespace; (g) ≥1 candidate steward in conversation. Depends on M0.

**M2 — Multi-source integration & reconciliation (breadth).**
Goal: add international funders, trial records, and outputs; reconcile and dedup across sources.
Exit criteria: (a) ≥4 total open sources integrated (NIH RePORTER + CORDIS + Gateway to Research +
AACT/ClinicalTrials.gov), each license-cleared; (b) funders reconciled to Crossref Funder Registry
(≥80%); outputs linked via OpenAlex/DOI; (c) cross-source org/effort **dedup workflow** operational
with human-confirmed merges and **zero confirmed false merges** in the audit sample; (d) study
records held strictly as aggregate registry metadata (no patient data) and verified so. Depends on
M1.

**M3 — Explorer, gaps ledger & family/advocate view (usable, honest surface).**
Goal: make the map browsable, honest about its blind spots, and safely useful to families/advocates.
Exit criteria: (a) public no-account explorer live, every assertion showing its source; (b) **"known
gaps" / coverage ledger** published and current; (c) data dictionary + usage/citation guide
published; (d) a **non-clinical** family/advocate orientation layer published, advocate-reviewed,
with the "not medical advice" notice; (e) reuse metrics tracked. Depends on M2.

**M4 — Scale, refresh automation & partner adoption (shipped).**
Goal: keep the map fresh and lock in real-world use.
Exit criteria: (a) **scheduled refresh** + staleness tracking operational (≥90% of refreshed
records within 90 days); (b) targets met (≥300 orgs, ≥1,500 grants, ≥150 study records across ≥4
sources) with 100% provenance maintained; (c) ≥1 steward has **adopted or cited** the map
(Definition of Shipped met); (d) sustainability/maintenance + reviewer-rotation plan in effect.
Depends on M3.

## Work breakdown

The itemized, schema-mapped backlog lives in [`TASKS.md`](./TASKS.md), organized by the milestones
above (M0–M4) plus a sized backlog. Each task maps to an Elyos Task JSON and carries a type, size,
risk tier, deliverable, dependencies, and reviewer. M0 deliberately front-loads the licensing,
scope, provenance, and PII guardrails before any bulk extraction begins.

## Governance, roles & stakeholders

- **Maintainer / Owner:** TBD — accountable for scope, the licensing/scope gates, and releases.
- **Source-license reviewer:** TBD — must approve every `sources/allowlist.yml` entry; has veto over
  any source; enforces the no-proprietary and no-patient-data boundaries. **Naming a qualified
  person is a hard M0 exit criterion.** **Documented fallback if the seat is empty:** no source
  advances past `pending` and no extraction begins; M0 cannot exit; the maintainer escalates to
  Elyos governance/board (and may engage pro-bono counsel) before any data work proceeds.
- **Domain / accuracy reviewers (rotation):** sarcoma/oncology researchers or experienced research
  analysts who validate the Ewing inclusion-query seed and perform accuracy/citation review.
  TO BE SECURED.
- **Patient-advocate reviewer:** required for any family/advocate-facing text (tone, "not advice"
  framing, non-clinical boundary). TO BE SECURED.
- **Steward (last-mile owner):** the advocacy/research org that adopts, hosts long-term, and cites
  the map. **TO BE SECURED** — required for "shipped."
- **Partner / requestor:** families, advocates, foundations, researchers (diffuse beneficiary
  class); a named representative org is TO BE SECURED.
- **Elyos governance/board:** arbiter for edge cases (e.g., a borderline source, a removal request)
  under the published conflict-of-interest / veto checklist.

## Dependencies & integrations

- **Open source systems:** NIH RePORTER/ExPORTER, EU CORDIS, UKRI Gateway to Research,
  ClinicalTrials.gov / **AACT** (CTTI), IRS 990 / ProPublica Nonprofit Explorer.
- **Identifier authorities:** ROR (CC0), Crossref Funder Registry (CC0), ORCID, NCT (NLM),
  DOI/Crossref, OpenAlex (CC0).
- **Reconciliation/linking:** OpenAlex, Wikidata/Wikipedia (CC0 / CC BY-SA).
- **Validation/serialization:** JSON-Schema, SHACL, RDF/JSON-LD tooling (TypeScript/ESM ecosystem).
- **FX rates:** a documented, citable open exchange-rate source for dated normalization.
- **Elyos pieces:** Task schema (`packages/schema`), CLI workspace/PR flow (`packages/cli`,
  `packages/core`), governance proposal/registry process. Donated lane — humans run their own
  agents; CLI never runs headless.
- **Sibling Ewing projects:** `ewing-open-data-catalog`, `ewsr1-fli1-knowledge-graph`,
  `ewing-trial-finder` (clinical interpretation lives there, behind expert review).

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |
| Contributor ingests proprietary research-intelligence data (Dimensions/WoS/Scopus/Candid), incl. laundered via a fake open citation | Medium | Critical (legal/ToS, project-ending) | Categorical out-of-scope rule; allow-list gate blocks un-approved sources; license-reviewer veto; CI rejects non-`approved` sources; **anti-laundering controls — record-level citations, contributor attestation, spot-checks for proprietary-distinctive fields**; refuse + flag | License reviewer |
| Patient-level / controlled-access data creeps in (e.g., a "richer" trial source) | Low | Critical (cancer guardrail breach) | Hard scope boundary; study records limited to aggregate registry fields; allow-list gate; reviewer checklist explicitly verifies "no patient data"; refuse + flag | License reviewer |
| Family/advocate text drifts into medical advice | Medium | High (safety/guardrail) | Non-clinical scope rule; standing "not medical advice" notice; mandatory patient-advocate review; clinical content redirected to `high`-risk siblings | Advocate reviewer |
| Wrong grant amount / currency / date (most damaging transparency error) | Medium | High | Original currency+amount always retained; dated-FX normalization provenanced; amount/currency a mandatory audit stratum; ≥95% accuracy gate | Domain reviewer |
| "Open" source actually carries restrictive API/redistribution terms | Medium | High | Per-channel rights analysis recorded in allow-list; verify the specific access channel and fields, not just "it's public" | License reviewer |
| No steward/partner secured → "delivered ≠ merged" not met | High | High | Treat partner outreach as an M0/M4 deliverable; log status honestly; pursue multiple candidate stewards | Maintainer |
| Bad/false entity merges corrupt the map (precision failure) | Medium | High | Precision-over-recall matcher; explicit blocking keys; canonical-ID anchoring (ROR/ORCID/Funder Registry); human-confirmed, reversible merges; zero-false-merge audit target | Domain reviewer |
| Stale data presented as current | Medium | Medium | Mandatory `retrievedAt` on every record; computed staleness surfaced; scheduled refresh in M4; freshness CI gate | Maintainer |
| Living-investigator data misuse / removal request | Low | Medium (privacy) | Public professional facts only; no contact/home/health data; documented correction/removal process; source-linked auditability; no ranking/dossier | License/domain reviewers |
| Ewing inclusion-query too broad/narrow → biased map | Medium | Medium | Published, version-controlled query; domain-reviewer-validated seed; precision/recall trade-off documented; gaps ledger states selection limits | Domain reviewer |
| Reviewer capacity exhausted / burnout | Medium | High | Sampling-based review (not 100% re-check); reviewer rotation with response-time SLA; documented throughput ceiling that throttles intake when backlog exceeds it | Maintainer |
| Mixed-license corpus mislabeled (CC BY/OGL attribution lost; CC0 vs CC BY-SA) | Medium | Medium | CC BY 4.0 default; per-source attribution strings recorded and surfaced; CC BY-SA text segregated; dataset-level license honesty | Maintainer |
| Implied endorsement / "scorecard" misuse of the map | Medium | Medium | Explicit no-ranking rule (no quality field in schema); usage guide states limits; map links, does not judge | Maintainer |

## Security & privacy

- **Threat surface:** small (data/content project, no accounts, no visitor PII). Main risks are
  *compliance* (illicit/patient sourcing) and *data integrity* (wrong/unsourced/stale assertions),
  addressed by the license, scope, accuracy, and freshness gates above.
- **Secrets handling:** open sources need no secrets; any API keys (e.g., a higher-rate-limit
  RePORTER/OpenAlex key) stay out of logs, receipts, and commits per Elyos rules. The donated lane
  never runs headless or authenticates an agent.
- **PII:** **no patient data, ever.** The only personal data is public professional facts about
  named investigators, with a correction/removal process; no contact/home/health/family data; no
  visitor tracking/profiling.
- **Abuse/misuse prevention:** every assertion is source-linked and auditable; the project refuses
  and flags any attempt to ingest proprietary-system data or any patient-level/controlled-access
  data; the schema carries **no ranking field**, so the map cannot be turned into a "scorecard" of
  people or institutions.

## Sustainability & maintenance

- **After delivery,** the maintainer plus the secured steward own ongoing curation; the steward
  provides long-term hosting, while the **canonical `ResearchEffort` persistent identifier
  (w3id.org/PURL) is owned by the project, not the host** — so identifiers survive a steward change
  and the map is never orphaned. All other entities anchor to external canonical IDs (ROR/ORCID/
  Funder Registry/NCT/DOI), which the project does not have to maintain.
- **Freshness:** a **scheduled refresh** re-pulls each approved source on its cadence, recomputes
  staleness, and re-runs the gates; stale records are flagged, never silently shown as current.
- **Reviewer sustainability:** review runs on **sampling, not exhaustive re-checking**; reviewers
  work a **rotation with a response-time SLA**; a **documented throughput ceiling** throttles new
  intake when the review backlog exceeds it, so quality gates never silently degrade under load.
- **Outcome tracking:** quarterly report on orgs/grants/study-records growth, provenance
  completeness (must stay 100%), reconciliation coverage, accuracy-audit pass rate, freshness, the
  gaps-ledger delta, partner adoptions, and reuse/downloads.
- **Contributions** continue via the donated lane under the same license + accuracy + (where
  applicable) advocate review gates.
- If no steward is secured, the project remains in a maintained-but-not-shipped state and the gap is
  reported honestly rather than declared done.

## Open questions

- Who is the committed steward / adopting partner? (TO BE SECURED — blocks "shipped.")
- Which patient-advocate organization staffs the family-facing review seat?
- Final provenance mechanism: named graphs + PROV-O vs. RDF-star? (Fixes the countable assertion
  unit — decided in M0.)
- Inclusion-query boundaries: include closely-adjacent fusion-family / "PNET/Askin" historical
  terminology, or restrict to modern *Ewing sarcoma* terms? (Domain-reviewer call in M0.)
- Which open FX-rate source is canonical for dated grant-amount normalization?
- How are non-English funder/foundation records (e.g., national charities outside NIH/CORDIS/UKRI)
  brought in without a paywalled aggregator? (Backlog candidate sources.)
- Default removal-request resolution when professional data is public but an individual objects —
  where is the public-interest line? (Governance/board policy.)

## References

- Project proposal: `governance/proposals/ewing-research-landscape.md` (**TO BE WRITTEN**)
- Elyos work rules: `CLAUDE.md`
- Good Deed Definition & risk tiers: `docs/good-deed-definition.md`
- Task JSON schema: `packages/schema/src/schemas.ts`
- Portfolio roadmap (Track 8a — Ewing): `planning/ROADMAP.md`
- Sibling sister-plan (architecture pattern): `planning/projects/revolutionary-patriots-kg/`
- Open sources: NIH RePORTER/ExPORTER (PD); EU CORDIS (CC BY 4.0); UKRI Gateway to Research (OGL
  v3.0); ClinicalTrials.gov / AACT (CTTI; PD records + acceptable-use terms); IRS 990 / ProPublica
  Nonprofit Explorer
- Identifier authorities: ROR (CC0), Crossref Funder Registry (CC0), ORCID, OpenAlex (CC0), NCT
  (NLM), DOI/Crossref; Wikidata (CC0) / Wikipedia (CC BY-SA 4.0)
- W3C: RDF, JSON-LD, SHACL, PROV-O, RDF-star

---

## Appendix A — Improvements applied

Twenty-five specific improvements were identified during drafting and are **already applied** in the
plan above (and mirrored in `TASKS.md`). This is a record of the hardening, not a to-do list.

1. **Led the data/licensing section with the binding cancer guardrails** (open/aggregate/org-level
   only; no controlled-access; no patient data) as Hard boundary 1, before any source list.
2. **Added a second hard boundary** making proprietary research-intelligence databases
   (Dimensions/WoS/Scopus/Candid) categorically out of scope, with anti-laundering controls.
3. **Per-source license recorded explicitly** (NIH PD, CORDIS CC BY 4.0, UKRI OGL v3.0,
   ClinicalTrials.gov/AACT PD + acceptable-use, ROR/Crossref/OpenAlex CC0) with a "verify at use
   time" caveat.
4. **Chose CC BY 4.0 as the data license** (not CC0) because CORDIS/UKRI attribution obligations
   propagate; CC0/PD components labeled, CC BY-SA text segregated.
5. **Mint IDs sparingly** — reuse ROR/ORCID/Funder Registry/NCT/DOI; mint only the composite
   `ResearchEffort` ID under a host-independent w3id.org/PURL namespace decoupled from the steward.
6. **Currency-normalization policy**: original currency+amount always retained as canonical; any
   normalized value carries FX rate/source/date as provenance; no silent conversion.
7. **Snapshot/freshness model**: every record carries `retrievedAt`; staleness computed and
   surfaced; freshness enforced as a CI gate and a scheduled-refresh task in M4.
8. **Published Ewing inclusion-query** as a first-class, version-controlled, domain-reviewer-
   validated artifact so "what counts as Ewing research" is reproducible and auditable.
9. **"Known gaps" / coverage ledger** made a required, recurring deliverable — a transparency tool
   must be honest about its own blind spots.
10. **No-ranking rule** baked into the schema (no quality field) so the map cannot be weaponized
    into a "best lab/funder" scorecard.
11. **Living-investigator privacy stance**: public professional facts only, with an explicit
    correction/removal process and no contact/home/health/family/dossier data.
12. **Family-facing content firewalled**: non-clinical orientation only, standing "not medical
    advice" notice, mandatory patient-advocate review; clinical interpretation redirected to the
    `high`-risk sibling projects.
13. **Accuracy-audit sampling frame pinned** (≥200 or whole release; stratified by source system
    and assertion type; independent auditor), with grant amount/currency a mandatory stratum.
14. **Zero-confirmed-false-merge** precision target with an explicit blocking-key strategy and
    canonical-ID anchoring, since a bad merge silently corrupts the map.
15. **AACT named as the preferred ClinicalTrials.gov intake** (clean bulk + clear terms) rather
    than scraping the site, with study records limited to aggregate registry fields.
16. **`verifiedNeed: false` everywhere** and "steward TO BE SECURED" stated honestly, with partner
    outreach made an M0/M4 deliverable and a precondition for "shipped."
17. **Source-license reviewer named as a hard M0 exit criterion** with a documented escalation
    fallback if the seat is empty (no extraction may begin).
18. **Reviewer-sustainability mechanics** added (sampling not exhaustive re-check; rotation with
    response-time SLA; documented throughput ceiling that throttles intake under backlog).
19. **Outcome-based success metrics** (sourced orgs/grants, provenance %, reconciliation coverage,
    accuracy pass rate, freshness, gaps ledger present, steward adoption) — explicitly *not* counts
    of PRs/commits/raw records.
20. **CI gate quartet** specified: schema + provenance-completeness + allow-list (no non-`approved`
    source) + freshness (every record dated).
21. **Conflict-faithful representation**: conflicting source values retained side by side with
    provenance; the map never silently picks a winner.
22. **Multi-currency, multi-jurisdiction reality** acknowledged (NIH USD, CORDIS EUR, UKRI GBP,
    national charities) instead of assuming one currency/country.
23. **Sibling-project boundaries drawn** (open-data-catalog, KG, trial-finder, family-guide) so
    this project stays low-risk and doesn't duplicate or absorb `high`-risk clinical work.
24. **"For families" framing** added up front with deliberate care — stating the project's purpose
    is orientation and dignity, never advice — and carried into beneficiaries and non-goals.
25. **Removal-request public-interest edge case** surfaced as an open question routed to the
    Elyos governance/board, rather than hand-waved.

## Review sign-off

**Reviewer:** Senior staff engineer + TPM (drafting agent), self-review pass.
**Date:** 2026-06-28. **Version reviewed:** 0.1.0.

**Completeness check (against PLAN_SPEC 17 sections):** all 17 required H2 sections present and in
order — Executive summary; Problem & beneficiaries (verified need = honest "gap real, partner TO BE
SECURED"); Goals/non-goals; Success metrics (baseline+target, outcome-based); Scope (explicit
out-of-scope incl. the two hard boundaries); Solution approach & architecture (pipeline, stack,
data model, key decisions); Data/licensing & compliance (**leads with cancer guardrails**, per-source
licenses, provenance, PII, attribution); Quality/review/risk gates (tier + reviewers + DoShipped +
DoD); Roadmap M0–M4 (each with measurable exit criteria + dependencies); Work breakdown (→TASKS.md);
Governance/roles; Dependencies; Risks table (13 rows, all five columns); Security & privacy;
Sustainability; Open questions; References. ✔

**Correctness check:**
- Cancer guardrails: open/aggregate/org-level only, no controlled-access, no patient data — stated
  as Hard boundary 1 and enforced via allow-list gate + reviewer checklist + refusal rule. ✔
- License specificity: each source's license named with a "verify at use time" caveat; data license
  CC BY 4.0 justified by CORDIS/UKRI attribution propagation. ✔
- Risk tier `low` defended, with the single escalation point (family-facing text) firewalled and the
  `high`-risk clinical work routed to siblings. ✔
- Schema alignment: every TASKS.md field traces to `packages/schema/src/schemas.ts`; the example
  Task JSON validated field-by-field (see TASKS.md sign-off). ✔
- Honesty: `verifiedNeed: false`, steward TO BE SECURED, proposal "TO BE WRITTEN," and outcome (not
  vanity) metrics — consistent throughout. ✔

**Fixes applied during review:** (a) added the freshness CI gate to the gate quartet (was implied,
now explicit); (b) added grant amount/currency as a *mandatory* audit stratum (a wrong figure is the
worst transparency error); (c) made the removal-request public-interest line an explicit open
question rather than an assumed policy; (d) corrected the data license rationale to name OGL/CC BY
propagation explicitly.

**Outstanding human decisions (cannot be resolved by the agent):** name the source-license reviewer
(hard M0 exit), secure a steward and a patient-advocate reviewer, write the governance proposal, and
ratify the inclusion-query boundary and FX source. These are tracked in Open questions and as M0
tasks. **Sign-off: APPROVED as Draft v0.1.0 for governance review** — not for data work until the
M0 license-reviewer seat is filled.
