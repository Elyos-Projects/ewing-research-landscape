# TASKS — ewing-research-landscape

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

Itemized backlog for the open map of the Ewing Sarcoma research ecosystem (organizations, efforts,
grants/awards, aggregate study records, outputs). See [`PLAN.md`](./PLAN.md) for context, the
binding cancer guardrails, the licensing gate, and the roadmap (M0–M4).

## How these tasks map to Elyos

Each task below becomes an Elyos **Task JSON** validated against
`packages/schema/src/schemas.ts`. Field mapping:

- **id** — stable `ewing-research-landscape-<area>-NNN` (the table ID).
- **title** — the table Title.
- **project** — `ewing-research-landscape`.
- **type** — one of `code | research | writing | data | design-spec | maintenance` (table "Type").
- **lane** — `donated` for all tasks here (the proposal's lane). Any future metered run would be
  `funded` and must add `fundedBudgetUsd`.
- **priority** — `high | medium | low`.
- **domain** — e.g. `["open-science","cancer-research","public-data","transparency","ewing-sarcoma"]`.
- **riskTier** — `low | medium | high`. License/extraction/reconciliation tasks are **low–medium**
  (license + accuracy gates); the family/advocate-facing task is **medium** (advocate review). No
  task here is `high`: clinical interpretation is **out of scope** and lives in sibling projects.
- **urgent** — boolean (default `false`).
- **deliverable** — `pr | dataset | document | translation` (table "Deliverable").
- **tokenEstimate** — `small | medium | large` (table "Size").
- **status** — `open | in-progress | review | delivered | done` (start `open`).
- **context / objective / acceptanceCriteria[] / resources[] / output** — per task.
- **requestor** — `jdev1977` / beneficiary class until a named partner is secured.
- **verifiedNeed** — **`false`** while no committed partner/steward is secured (honest; the *gap* is
  real but the last-mile beneficiary is TO BE SECURED).
- **outputLicense** — `MIT` (code), `CC-BY-4.0` (data/docs default), or `CC0-1.0` where a deliverable
  is derived purely from CC0/PD sources.

> **Standing guardrails on every data/extraction task** (binding, per PLAN.md):
> 1. No source may be touched until its `sources/allowlist.yml` entry is `approved` by the
>    source-license reviewer.
> 2. **Open-access / aggregate / organization-/award-level data only.** Any task proposing to use
>    controlled-access data (dbGaP, EGA), individual-level biobank/clinical data, **any identifiable
>    patient data**, or a proprietary research-intelligence database (Dimensions/WoS/Scopus/Candid)
>    is **refused and flagged** — out of scope, full stop.
> 3. No medical advice / no clinical interpretation; any family-facing text is non-clinical,
>    "not medical advice," and patient-advocate reviewed.

---

## Milestone M0 — Foundation, scope & compliance spine

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ewing-research-landscape-model-001 | Define core data model (Org/Person/Grant/Effort/StudyRecord/Output) mapped to schema.org/ROR/Crossref/NCT/DOI | design-spec | small | low | document | — | Maintainer + domain reviewer |
| ewing-research-landscape-license-001 | Source allow-list schema + licensing-gate + cancer-guardrail + no-proprietary policy | design-spec | small | medium | document | — | License reviewer |
| ewing-research-landscape-prov-001 | Ratify provenance mechanism + countable assertion unit + currency-normalization + freshness policy | design-spec | small | low | document | ewing-research-landscape-model-001 | Maintainer |
| ewing-research-landscape-id-001 | Persistent-ID reuse policy (ROR/ORCID/Funder Registry/NCT/DOI; mint only Effort IDs on w3id.org/PURL) | design-spec | small | low | document | ewing-research-landscape-model-001 | Maintainer |
| ewing-research-landscape-privacy-001 | Living-investigator data + correction/removal policy | design-spec | small | medium | document | ewing-research-landscape-model-001 | License reviewer |
| ewing-research-landscape-scope-001 | Define + publish the reproducible Ewing inclusion-query (seed list validated) | research | small | medium | document | ewing-research-landscape-model-001 | Domain reviewer |
| ewing-research-landscape-ci-001 | CI scaffold: schema + provenance-completeness + allow-list + freshness gates | code | medium | low | pr | ewing-research-landscape-model-001, ewing-research-landscape-prov-001 | Maintainer |
| ewing-research-landscape-partner-001 | Steward + domain/advocate-reviewer outreach (status logged) | research | small | low | document | — | Maintainer |

**Acceptance criteria (key M0 tasks)**

- **ewing-research-landscape-model-001**
  - All core entities (Organization, Person, Grant/Award, ResearchEffort, StudyRecord, Output,
    Source, Place) defined with properties, datatypes, and cardinality.
  - Each entity/property maps to a canonical vocabulary/ID (schema.org, ROR, ORCID, Crossref Funder
    Registry, NCT, DOI/OpenAlex) where one exists; gaps documented.
  - Grant carries original-currency + amount as canonical, with a separate optional normalized field.
  - **No quality/ranking field exists** (no-scorecard rule); conflicting-value representation
    specified (no forced single "truth").
  - Every entity reserves a provenance slot (source IRI + license + `retrievedAt`).
- **ewing-research-landscape-license-001**
  - `sources/allowlist.yml` schema defines: name, custodian, URL/API, format, license + license URL,
    redistribution terms, attribution string, refresh cadence, and `status: approved|rejected|pending`.
  - Policy categorically `rejects` (a) any patient-level/controlled-access data and (b) proprietary
    research-intelligence databases; anti-laundering controls (record-level citations, contributor
    attestation, proprietary-distinctive-field spot-checks) are specified.
  - Per-access-channel rights-verification requirement documented ("open record" ≠ "open API terms").
- **ewing-research-landscape-scope-001**
  - The Ewing inclusion-query (MeSH/keyword terms + curated org/consortium seed) is written, version
    controlled, and **validated by a domain reviewer**.
  - Precision/recall trade-offs and boundary decisions (e.g., PNET/Askin historical terms) are
    documented; selection limits are slated for the gaps ledger.
- **ewing-research-landscape-ci-001**
  - CI fails on any assertion lacking a provenance link.
  - CI rejects data referencing a source not marked `approved`.
  - CI fails on any record missing a `retrievedAt` snapshot date.
  - CI validates records against the schema/SHACL shapes.

**M0 Definition of Done:** data model v0 published; allow-list schema + cancer-guardrail/no-proprietary
policy merged with ≥3 sources analyzed and ≥1 `approved`; provenance mechanism + assertion unit +
currency + freshness policies ratified; persistent-ID reuse policy committed (w3id.org/PURL for Effort
IDs); living-investigator + removal policy published; reproducible Ewing inclusion-query published and
domain-validated; CI gate quartet live; steward/reviewer outreach initiated with status logged;
**a qualified source-license reviewer named (hard exit; if the seat is empty M0 cannot exit — escalate
per the documented fallback in PLAN.md)**. `pnpm build && pnpm test && pnpm lint` green.

---

## Milestone M1 — First sourced slice (NIH RePORTER)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ewing-research-landscape-extract-001 | Build NIH RePORTER Ewing extractor (deterministic, flag-on-doubt) | code | medium | low | pr | ewing-research-landscape-ci-001, ewing-research-landscape-license-001, ewing-research-landscape-scope-001 | Maintainer |
| ewing-research-landscape-data-001 | Extract Ewing NIH award batch → Org/Grant/Person/Effort records with provenance | data | large | medium | dataset | ewing-research-landscape-extract-001 | Domain reviewer |
| ewing-research-landscape-recon-001 | ROR reconciliation for institutions/funders (human-confirmed) | data | medium | medium | dataset | ewing-research-landscape-data-001 | Domain reviewer |
| ewing-research-landscape-qa-001 | Accuracy/citation audit of M1 batch (stratified, ≥95% verified) | research | small | medium | document | ewing-research-landscape-data-001 | Domain reviewer |
| ewing-research-landscape-export-001 | CSV + JSON-LD export tooling under the persistent-ID namespace | code | medium | low | pr | ewing-research-landscape-data-001 | Maintainer |

**Acceptance criteria (key M1 tasks)**

- **ewing-research-landscape-extract-001**
  - Pulls only from the `approved` NIH RePORTER channel using the published inclusion-query.
  - Extraction is deterministic and assistive: maps authoritative fields; **never infers** unknown
    values; ambiguous fields are flagged for human review.
  - Records the extraction method and `retrievedAt` into every assertion's provenance.
- **ewing-research-landscape-data-001**
  - Ewing-relevant NIH awards mapped to Organization/Grant/Person/ResearchEffort records.
  - **100%** of new assertions carry a resolvable provenance link (source record URL + license +
    `retrievedAt`); passes the CI gate quartet before review.
  - **100%** of grants retain original currency + amount; any normalized value carries FX
    rate/source/date.
  - Conflicting source values retained with separate provenance; gaps remain gaps (logged).
  - **No patient data**: only award/organization/investigator-professional fields are stored
    (reviewer verifies).
- **ewing-research-landscape-recon-001**
  - Institutions/funders matched to ROR via an explicit blocking-key strategy (precision over recall).
  - No automatic merge ships without human confirmation; merges reversible and provenance-preserving.
  - **Zero confirmed false merges** in the dedup audit sample; ≥85% of institutions/funders carry a
    ROR ID.
- **ewing-research-landscape-qa-001**
  - A **stratified** sample (min ≥200 or whole release; strata by source system and assertion type,
    with grant amount/currency a mandatory stratum) is checked against the cited record; ≥95% verify.
  - The **auditor is independent of the extractor** of the sampled records.
  - Citations checked are record-level (database-level citations rejected); errors block sign-off.

**M1 entry precondition (hard gate):** the NIH RePORTER access path + its public-domain terms are
recorded `approved` in the allow-list, and the Ewing inclusion-query is published, before extraction
begins.

**M1 Definition of Done:** end-to-end pipeline proven on one approved NIH source; 100% provenance +
snapshot dates; ≥85% ROR coverage; 100% original currency retained; stratified accuracy audit (≥200,
independent auditor) ≥95%; CSV + JSON-LD exports produced under the persistent-ID namespace; ≥1
candidate steward in conversation.

---

## Milestone M2 — Multi-source integration & reconciliation

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ewing-research-landscape-data-002 | Integrate EU CORDIS (CC BY) + UKRI Gateway to Research (OGL) funders | data | large | medium | dataset | ewing-research-landscape-export-001, ewing-research-landscape-license-001 | Domain + license reviewers |
| ewing-research-landscape-data-003 | Integrate AACT/ClinicalTrials.gov study records as aggregate metadata only | data | medium | medium | dataset | ewing-research-landscape-export-001, ewing-research-landscape-license-001 | License + domain reviewers |
| ewing-research-landscape-recon-002 | Crossref Funder Registry reconciliation + OpenAlex/DOI output linking | data | medium | medium | dataset | ewing-research-landscape-data-002 | Domain reviewer |
| ewing-research-landscape-dedup-001 | Cross-source org/effort dedup workflow (human-confirmed, reversible) | code | medium | medium | pr | ewing-research-landscape-recon-002 | Maintainer + domain reviewer |

**Acceptance criteria (key M2 tasks)**

- **ewing-research-landscape-data-003**
  - Study records hold **only aggregate registry metadata** (NCT ID, title, sponsor, phase, status,
    public summary). **No participant/patient data** of any kind (reviewer verifies explicitly).
  - Sourced via the `approved` AACT/ClinicalTrials.gov channel; acceptable-use terms respected (no
    implied endorsement); 100% provenance + `retrievedAt`.
- **ewing-research-landscape-dedup-001**
  - Cross-source duplicates anchored on canonical IDs (ROR/Funder Registry/NCT/DOI) plus blocking
    keys; matcher tuned for precision over recall.
  - No automatic merge ships without human confirmation; merges reversible and provenance-preserving.
  - **Zero confirmed false merges** in the dedup audit sample.

**M2 Definition of Done:** ≥4 total open sources integrated (NIH + CORDIS + GtR + AACT), each
license-cleared with attributions recorded; funders ≥80% reconciled to Crossref Funder Registry;
outputs linked via OpenAlex/DOI; cross-source dedup operational with zero confirmed false merges;
study records verified as aggregate-only (no patient data); 100% provenance maintained.

---

## Milestone M3 — Explorer, gaps ledger & family/advocate view

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ewing-research-landscape-explorer-001 | Static public explorer over JSON-LD (no accounts/PII; every assertion shows its source) | code | medium | low | pr | ewing-research-landscape-dedup-001 | Maintainer |
| ewing-research-landscape-docs-001 | "Known gaps" / coverage ledger + data dictionary + usage/citation guide | writing | small | low | document | ewing-research-landscape-explorer-001 | Maintainer + domain reviewer |
| ewing-research-landscape-family-001 | Non-clinical family/advocate orientation layer ("not medical advice", advocate-reviewed) | writing | small | medium | document | ewing-research-landscape-explorer-001 | Patient-advocate reviewer |
| ewing-research-landscape-metrics-001 | Reuse-metrics tracking (downloads/queries) | maintenance | small | low | document | ewing-research-landscape-explorer-001 | Maintainer |

**Acceptance criteria (key M3 tasks)**

- **ewing-research-landscape-docs-001**
  - A "known gaps" ledger states honestly what is and is not covered (sources excluded, inclusion-
    query limits, regions/funders under-represented), updated each release.
  - Data dictionary documents every field + its source + license; usage guide states the
    no-ranking/no-advice limits and the required attributions.
- **ewing-research-landscape-family-001**
  - Strictly **non-clinical orientation** (who funds/works on Ewing; how to read the map); carries a
    standing **"This is not medical advice"** notice and links every statement to its source.
  - **Patient-advocate reviewed** before publish; any content that interprets a treatment/trial for a
    patient is removed and redirected to the `high`-risk sibling projects.

**M3 Definition of Done:** public no-account explorer live (every assertion source-linked); "known
gaps" ledger published and current; data dictionary + usage/citation guide published; non-clinical
family/advocate layer published and advocate-reviewed; reuse metrics tracked.

---

## Milestone M4 — Scale, refresh automation & partner adoption (shipped)

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| ewing-research-landscape-refresh-001 | Scheduled refresh + staleness tracking across approved sources | code | medium | low | pr | ewing-research-landscape-explorer-001 | Maintainer |
| ewing-research-landscape-data-004 | Scale to targets (≥300 orgs / ≥1,500 grants / ≥150 study records across ≥4 sources) | data | large | medium | dataset | ewing-research-landscape-dedup-001, ewing-research-landscape-license-001 | Domain + license reviewers |
| ewing-research-landscape-partner-002 | Secure steward adoption + ≥1 documented citation/use | research | medium | low | document | ewing-research-landscape-partner-001 | Maintainer |
| ewing-research-landscape-sustain-001 | Sustainability, hosting + reviewer-rotation/throughput plan | writing | small | low | document | ewing-research-landscape-partner-002 | Maintainer |

**Acceptance criteria (key M4 tasks)**

- **ewing-research-landscape-refresh-001**
  - Each approved source re-pulled on its recorded cadence; staleness recomputed; gates re-run.
  - Stale records flagged (never silently shown as current); ≥90% of refreshed records within 90 days.
- **ewing-research-landscape-partner-002**
  - A named advocacy/research steward commits to adopt/host and cite the map.
  - ≥1 concrete citation or downstream use is documented.

**M4 Definition of Done (project "shipped"):** targets met (≥300 orgs / ≥1,500 grants / ≥150 study
records across ≥4 sources) with 100% provenance and original currency retained; scheduled refresh +
freshness operational; ≥1 steward has adopted/cited the map; persistence/sustainability + reviewer-
rotation plan in effect; any family-facing text advocate-reviewed.

---

## Backlog / future (sized, unscheduled)

| ID | Title | Type | Size | Risk | Deliverable | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| ewing-research-landscape-data-005 | Integrate IRS 990 / ProPublica Nonprofit Explorer (US foundations) | data | medium | medium | dataset | Public filings; verify access-channel terms |
| ewing-research-landscape-data-006 | Add non-English national-charity funders (no paywalled aggregator) | data | large | medium | dataset | Open question: sourcing without proprietary aggregators |
| ewing-research-landscape-wikidata-001 | Wikidata round-trip (push reconciled ROR/ORCID/Funder links) | data | medium | low | dataset | CC0; strengthens open-data graph |
| ewing-research-landscape-viz-001 | Funder→institution→effort network visualization (no ranking) | code | medium | low | pr | Read-only over exports; no scorecard |
| ewing-research-landscape-quality-001 | Automated anomaly/outlier flagging for review (assistive) | code | medium | low | pr | Human-confirmed; never auto-edits |
| ewing-research-landscape-i18n-001 | Multilingual org/funder labels via Wikidata | data | small | low | dataset | CC0 labels |

---

## Example task JSON

Schema-valid Task JSON for the first M0 task (`ewing-research-landscape-model-001`), validated
field-by-field against `packages/schema/src/schemas.ts`:

```json
{
  "id": "ewing-research-landscape-model-001",
  "title": "Define core data model (Org/Person/Grant/Effort/StudyRecord/Output) mapped to schema.org/ROR/Crossref/NCT/DOI",
  "project": "ewing-research-landscape",
  "type": "design-spec",
  "lane": "donated",
  "priority": "high",
  "domain": ["open-science", "cancer-research", "public-data", "transparency", "ewing-sarcoma"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "small",
  "status": "open",
  "context": "An open, source-linked map of the Ewing Sarcoma research ecosystem (organizations, grants/awards, research efforts, aggregate registered-study records, and public outputs) needs a shared data model before any data is ingested. Binding cancer guardrails: open-access / aggregate / organization-/award-level data ONLY -- no controlled-access (dbGaP, EGA), no individual-level biobank/clinical data, no identifiable patient data; proprietary research-intelligence databases (Dimensions/WoS/Scopus/Candid) are out of scope. Sources are open only (NIH RePORTER PD, CORDIS CC BY, UKRI OGL, ClinicalTrials.gov/AACT PD, ROR/Crossref/OpenAlex CC0). See PLAN.md.",
  "objective": "Define the core entities (Organization, Person, Grant/Award, ResearchEffort, StudyRecord, Output, Source, Place) and their properties, reusing canonical vocabularies/IDs (schema.org, ROR, ORCID, Crossref Funder Registry, NCT, DOI/OpenAlex) wherever an equivalent exists, retaining original grant currency/amount, and deliberately omitting any quality/ranking field.",
  "acceptanceCriteria": [
    "All core entities defined with properties, datatypes, and cardinality.",
    "Each entity/property mapped to a schema.org/ROR/ORCID/Crossref/NCT/DOI equivalent where one exists; gaps documented.",
    "Grant carries original currency + amount as canonical, with a separate optional FX-normalized field.",
    "No quality/ranking field exists (no-scorecard rule); conflicting-value representation specified (no forced single truth).",
    "StudyRecord holds aggregate registry metadata only -- no participant/patient fields.",
    "Every entity reserves a provenance slot (source IRI + license + retrievedAt) per the provenance model.",
    "Published as a human-readable spec plus a machine artifact (JSON-Schema/SHACL stub)."
  ],
  "resources": [
    "planning/projects/ewing-research-landscape/PLAN.md",
    "https://schema.org/",
    "https://ror.org/",
    "https://www.crossref.org/services/funder-registry/",
    "https://orcid.org/"
  ],
  "output": "A data-model specification document (model/README.md) plus a JSON-Schema/SHACL stub defining the core entities and their schema.org/ROR/Crossref/NCT/DOI mappings, committed via PR.",
  "requestor": "jdev1977",
  "verifiedNeed": false,
  "outputLicense": "CC-BY-4.0"
}
```

## Review sign-off

**Reviewer:** drafting agent self-review, 2026-06-28, against `packages/schema/src/schemas.ts`.

- **Schema validity:** the example JSON includes all 16 `required` fields; every enum value is legal
  (`type: design-spec`, `lane: donated`, `priority: high`, `riskTier: low`, `deliverable: document`,
  `tokenEstimate: small`, `status: open`); `acceptanceCriteria` has ≥1 item; `output` is non-empty;
  `domain` is a string array; no `additionalProperties`. `lane` is `donated`, so `fundedBudgetUsd`
  is correctly omitted (the `if/then` only requires it for `funded`). ✔
- **Honesty:** `verifiedNeed: false` on all tasks (no steward secured); proposal "TO BE WRITTEN." ✔
- **Coverage:** 21 scheduled tasks across M0–M4 + 6 backlog = 27 sized items; each milestone has a
  task table, key-task acceptance criteria, and a Definition of Done matching PLAN.md's roadmap. ✔
- **Risk discipline:** no `high`-risk task here — clinical interpretation is out of scope and routed
  to sibling projects; the single `medium`-on-safety task (family-001) requires patient-advocate
  review. ✔

---

## Generated task index

Every table row above is now backed by a schema-valid `tasks/<id>.json` (validated against
`packages/schema` taskSchema: all enums legal, `filename == id`, no duplicate ids, no extra keys).
Each JSON carries the row's full `acceptanceCriteria` — the key-task criteria above are reused
verbatim, and rows that listed no explicit criteria here had checkable criteria derived from their
title + the milestone Definition of Done. `tasks/*.json` is the executable source of truth for the
Elyos CLI; this table remains the human-readable backlog.

**Fan-out:** none. Each named source (NIH RePORTER, EU CORDIS, UKRI GtR, AACT/ClinicalTrials.gov,
IRS 990/ProPublica, Wikidata) already has its own dedicated backlog row, so each becomes one task —
no row was multiplied across an enumerated dimension and no languages/datasets/beneficiaries were
fabricated. Where a dimension is open-ended (`data-006` non-English funders; partner/steward "TO BE
SECURED"), one representative task is emitted and expands on scope/partner confirmation.

**Guardrails preserved in the JSONs:** the binding cancer guardrail (open/aggregate/org-/award-level
data only; no controlled-access/patient/individual-level data; no proprietary research-intelligence
databases; no medical advice/clinical interpretation) is carried in the `context` of every
data/extraction task and the family layer; `data-006` explicitly *refuses* paywalled/proprietary
aggregators. `verifiedNeed:false` on all tasks (no steward/partner secured yet).

| Milestone | Task IDs (`ewing-research-landscape-*`) |
| --- | --- |
| M0 | `model-001` (seed), `license-001`, `prov-001`, `id-001`, `privacy-001`, `scope-001`, `ci-001`, `partner-001` |
| M1 | `extract-001`, `data-001`, `recon-001`, `qa-001`, `export-001` |
| M2 | `data-002`, `data-003`, `recon-002`, `dedup-001` |
| M3 | `explorer-001`, `docs-001`, `family-001`, `metrics-001` |
| M4 | `refresh-001`, `data-004`, `partner-002`, `sustain-001` |
| Backlog | `data-005`, `data-006`, `wikidata-001`, `viz-001`, `quality-001`, `i18n-001` |

Total: 31 task files (1 pre-existing seed + 30 generated).
