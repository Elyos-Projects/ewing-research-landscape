# Competitive & Improvement Analysis — `ewing-research-landscape`

Rigorous review of the Elyos cancer-research good-deed project: an open, source-linked map of the
Ewing Sarcoma research ecosystem (orgs, funders/grants, registered studies, advocacy groups) built
from open sources (NIH RePORTER, ClinicalTrials.gov/AACT, CORDIS, UKRI GtR, OpenAlex, ROR, IRS 990).
Reviewed against `PLAN.md` v0.1.0 and `TASKS.md` v0.1.0 (both 2026-06-28). Web sources cited inline.

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually mature: it leads with the binding cancer guardrails, separates this low-risk
mapping project from the high-risk clinical siblings, mandates record-level provenance, bans
ranking, reuses canonical IDs, and is honest that no steward is secured (`verifiedNeed: false`).
The 25-item "improvements applied" appendix and the stratified accuracy-audit frame are genuine
strengths. That said, there are concrete gaps, errors, and weak spots:

**Data-source / sourcing gaps**

- **World RePORT is missing and it is the closest real competitor.** NIH Fogarty's
  [World RePORT](https://worldreport.nih.gov/) already does cross-funder mapping (NIH, UK MRC,
  Wellcome, Gates, European Commission, CIHR) with a map UI. The plan never mentions it. It must be
  in the competitive landscape *and* mined as a source/reconciliation target — not knowing about it
  is a credibility gap for a "transparency map" project.
- **No non-US/EU funder strategy beyond a backlog stub.** The four anchor sources (NIH, CORDIS,
  UKRI, AACT) are entirely US + EU/UK. Germany (DFG, GPOH/the historical Ewing trial home), France
  (INCa), Spain, Australia (NHMRC), Canada (CIHR), Japan, and the large disease-specific charities
  are where much Ewing work actually sits. The plan acknowledges this only as open question +
  backlog task `data-006`. For a *rarity-driven, internationally fragmented* disease (research is
  ~3 cases/million/yr and explicitly "fragmented across many countries" —
  [Oncotarget summit](https://www.oncotarget.com/article/6937/text/)), a US/EU-only v1 risks
  systematically *under-mapping the gaps it claims to surface* — a fairness/neutrality problem, not
  just a coverage one. The gaps ledger mitigates honesty but not the skew.
- **Foundation/990 coverage is under-powered and mis-scoped.** The richest picture of small
  Ewing/sarcoma family foundations is in their own grant announcements (e.g.
  [QuadW](https://www.quadw.org/sarcoma-research),
  [Sarcoma Foundation of America](https://curesarcoma.org/research/funding-opportunities/),
  [St. Baldrick's hero funds](https://www.stbaldricks.org/hero-funds/mistercheeks/)), which are
  *not* in IRS 990s in any structured, grant-level, Ewing-tagged way. 990 Schedule I lists grantees
  but rarely the research topic, often routes through intermediaries (AACR, St. Baldrick's), and
  lags 1–2 years. Treating ProPublica 990 as the foundation source (backlog `data-005`) will
  badly under-count and mis-attribute the long tail. The plan needs an explicit, license-checked
  "foundation public grant-listing" intake distinct from 990s.
- **OpenAlex is under-used.** OpenAlex carries works *and* funder/grant linkage and is CC0
  ([OpenAlex about](https://help.openalex.org/hc/en-us/articles/24396686889751-About-us)); the plan
  uses it only for output linking and reconciliation. It could also be a *grant-discovery* and
  *cross-funder* source, partially substituting for the proprietary Dimensions grant graph the plan
  rightly refuses. Under-leveraging the strongest free asset is a missed-opportunity gap.

**Entity / data-model issues**

- **Person disambiguation is the weakest reconciliation link and the plan glosses it.** ROR
  reconciliation gets a hard 85% target and a blocking-key strategy; ORCID matching of investigators
  gets neither a target nor a method. ORCID coverage of grant PIs is partial and uneven across
  countries; many RePORTER/CORDIS records lack ORCIDs. Name-only matching of common surnames is
  exactly where false merges (and privacy harm) happen. There should be a stated PI-matching
  precision policy and an explicit "leave unmatched rather than guess" rule.
- **"Effort" minting may create duplicate-effort sprawl.** `ResearchEffort` is the one minted-ID
  composite node tying grants↔people↔studies↔outputs. Without a crisp rule for when two grants are
  "the same effort" vs. two efforts, the precision-over-recall stance (good for ROR) can *over-split*
  efforts, fragmenting the very picture the map promises. A merge/split policy for Effort is needed.
- **Currency normalization omits time-of-award vs. spend-year ambiguity.** Dated FX is good, but the
  plan doesn't say *which* date (award start? obligation year? each fiscal-year tranche?) anchors the
  rate, nor how multi-year awards are handled. Inconsistent date-anchoring silently distorts
  cross-funder comparisons — the single most damaging error class the plan itself names.

**Metric / measurement weaknesses**

- **Targets are absolute counts with no precision/recall denominator.** "≥300 orgs, ≥1,500 grants,
  ≥150 study records" measures *volume*, not *coverage of the true population*. The plan explicitly
  disavows count-as-success in prose, yet the headline scorecard is counts. There is no
  recall/completeness estimate (e.g., "we captured N of an estimated M Ewing trials on
  ClinicalTrials.gov"). For a *gaps* tool, a coverage-against-a-known-frame metric (e.g., all
  active CTG trials matching the published query) matters more than raw totals.
- **"≥95% accuracy" has no error-severity weighting.** A wrong ROR link and a wrong grant amount are
  both "1 error," but the plan says amounts are the worst error. The audit should weight or separately
  gate amount/currency errors (e.g., zero tolerance band), not fold them into one 95%.
- **Freshness target (`≥90% within 90 days`) is unrealistic for 990s/foundation pages.** 990 filings
  publish 12–18 months late; foundation pages update irregularly. A single global freshness SLA will
  fail on the slowest-moving sources. Freshness needs to be per-source-cadence, not one number.

**Neutrality / endorsement / value-judgment risks**

- **"Known gaps" + "where the white space is" is itself an implicit value judgment.** Stating a
  subtopic or region is "under-funded" or a "gap" can read as advocacy/criticism of specific funders.
  The no-ranking rule covers entities but not *narrative framing of gaps*. The gaps ledger needs a
  neutrality rubric: descriptive ("no awards in source X match query Y") not evaluative
  ("Ewing is neglected"). ClinicalTrials.gov/AACT terms also forbid implying endorsement —
  ([AACT/CTTI](https://aact.ctti-clinicaltrials.org/)) — the explorer copy must be audited for this.
- **Selection = endorsement risk.** Deciding an org/effort "counts as Ewing" via the inclusion query
  is itself a judgment that can offend excluded small foundations. Plan handles reproducibility but
  not the *appeals/inclusion-request* path symmetric to the removal path.

**Privacy / licensing**

- **Living-investigator removal vs. public-interest line is unresolved** (the plan honestly flags it
  as open). But it under-specifies the *default during dispute*: is the record hidden pending review
  or shown? GDPR/UK-GDPR legitimate-interest analysis for EU/UK PIs is asserted as "low" but not
  actually performed; CORDIS/GtR PI data are personal data under GDPR and deserve a recorded LIA.
- **Aggregated-DB copyright on the *output*, not just inputs.** The plan guards against ingesting
  proprietary DBs, but doesn't address that *its own* compiled CC-BY dataset could be re-wrapped by a
  proprietary product — a CC-BY-SA (ShareAlike) or explicit anti-enclosure clause merits a decision,
  not silence. (CC-BY allows commercial re-enclosure of the compilation.)
- **Wikipedia CC-BY-SA contamination risk** is noted but the firewall mechanism (how SA text is kept
  out of the CC-BY corpus in practice) is not specified beyond "segregated."

**Process / scope**

- **No de-duplication against sibling `ewing-open-data-catalog` / KG** — overlap boundaries are named
  but not operationalized; risk of two Elyos projects mapping the same orgs divergently.
- **Steward risk is correctly flagged as High/High but has no plan-B success definition** — if no
  steward ever signs, "maintained-but-not-shipped" is stated, but there's no minimum public-good
  threshold (e.g., "dataset is cited by ≥1 researcher") that would still count as a partial win.

---

## 2. Competitive landscape (real tools, cited)

**Open infrastructure & sources (also competitors for "the integrated view")**

- **NIH RePORTER / RePORT** — [report.nih.gov](https://report.nih.gov/). Free, weekly-updated US
  federal biomedical grant search (NIH + CDC, AHRQ, HRSA, ACF, VA), with publication/patent links.
  *Strengths:* authoritative, public-domain, granular, API. *Weaknesses:* US-only; no foundation,
  EU, trial, or advocacy data; no Ewing-specific view; not reconciled to ROR/Funder Registry; no
  cross-source linking; family-hostile UI.
- **World RePORT (NIH Fogarty)** — [worldreport.nih.gov](https://worldreport.nih.gov/). **The closest
  direct analogue:** open, interactive map of *global* biomedical investments across NIH, UK MRC,
  Wellcome, Gates, EC, CIHR. *Strengths:* genuinely multi-funder + international + mapped; open
  access. *Weaknesses:* only ~6 large funders (no small/family foundations, no trials, no
  ClinicalTrials.gov, no advocacy orgs); data from 2016+; not disease-specific; not source-linked at
  assertion level; not a reusable openly-licensed dataset with persistent IDs.
- **ClinicalTrials.gov / AACT (CTTI)** — [aact.ctti-clinicaltrials.org](https://aact.ctti-clinicaltrials.org/),
  [GitHub](https://github.com/ctti-clinicaltrials/aact). Public-domain registry; AACT gives free,
  daily, well-documented bulk download (40+ tables). *Strengths:* authoritative trials, bulk, clean.
  *Weaknesses:* trials only; not linked to grants/funders/outputs; acceptable-use forbids implied
  endorsement; sponsor names un-reconciled to ROR.
- **OpenAlex (OurResearch)** — [openalex.org](https://help.openalex.org/hc/en-us/articles/24396686889751-About-us).
  474M works linked to authors, institutions, funders; fully CC0, quarterly snapshots, free API.
  *Strengths:* the open replacement for Scopus/WoS; funder + grant linkage; CC0. *Weaknesses:*
  publication-centric (grants/funding metadata thinner and noisier than Dimensions); no trials, no
  990s; affiliation/funder disambiguation imperfect; not disease-curated.
- **ROR** — [ror.org](https://ror.org/about/). 120k+ org CC0 persistent IDs via open API.
  *Strengths:* the org-disambiguation backbone; CC0; community-run (Crossref/DataCite/CDL).
  *Weaknesses:* orgs only (no people/grants/trials); small foundations under-represented; not a
  funding/landscape product — it's plumbing the project should consume.
- **Crossref Funder Registry** — CC0 funder IDs ([Crossref/ROR](https://www.crossref.org/community/ror/));
  being merged toward ROR. Plumbing, not a competitor; reconciliation target.
- **Gateway to Research (UKRI)** — [gtr.ukri.org](https://gtr.ukri.org/). UK public-funded research
  under OGL v3.0, JSON/XML API, reuse incl. commercial
  ([GtR API](https://gtr.ukri.org/resources/gtrapi2.html)). *Strengths:* open, structured, UK
  authoritative. *Weaknesses:* UK only; no trials/foundations; not Ewing-curated.
- **EU CORDIS** — CC BY 4.0 EU-funded projects (attribution required). *Strengths:* EU authoritative,
  openly licensed, bulk. *Weaknesses:* EU framework programmes only; no national charities; no trials.

**Proprietary research-intelligence (the paywalled integrated view the project undercuts)**

- **Dimensions.ai (Digital Science)** — [dimensions.ai](https://www.dimensions.ai/). 140M+ pubs
  linked to ~7.1M grants ($2.6T), patents, trials, policy. *Strengths:* the best integrated
  grants↔pubs↔trials graph. *Weaknesses:* org/funder analytics and bulk are subscription
  (~$10k–$50k/yr per [UCSF guide](https://guides.ucsf.edu/dimensions)); license forbids
  redistribution — families/small foundations can't get or reshare it. Free tier is pubs-only.
- **Candid (Foundation Directory Online + GuideStar)** — [candid.org](https://candid.org/). 1.9M
  orgs, 3M grant transactions, $180B/yr. *Strengths:* deepest US foundation/990 grant data.
  *Weaknesses:* core depth is paywalled; redistribution forbidden; not research- or Ewing-specific.
- **Web of Science / Scopus** — citation DBs behind institutional licenses; no grant/trial/foundation
  integration for the public; redistribution forbidden. Categorically out-of-scope as sources.

**Adjacent funder/landscape efforts**

- **Chan Zuckerberg Initiative grants database** — [CZI grants](https://chanzuckerberg.com/grants-ventures/grants/),
  [open-science grantees](https://chanzuckerczi.github.io). Public funder-specific grant disclosure.
  *Strength:* model for open self-disclosure. *Weakness:* one funder; not a cross-ecosystem map.
- **Sarcoma/Ewing foundations' own listings** — QuadW, SFA/CureSarcoma, St. Baldrick's hero funds,
  Northwest Sarcoma, Slifka, AACR-QuadW fellowship pages (cited above). *Strengths:* primary,
  authoritative for their own grants. *Weaknesses:* HTML pages, no IDs, no machine format, no
  cross-org view, inconsistent, often no amounts/topics — exactly the fragmentation this project
  consolidates.
- **Bibliometric/text-mining Ewing reviews** — e.g. [BMC Cancer 1993–2022 bibliometrics](https://link.springer.com/article/10.1186/s12885-023-10723-7),
  [Annals Surg Oncol text-mining](https://link.springer.com/article/10.1245/s10434-025-16978-7).
  *Strengths:* academic landscape snapshots. *Weaknesses:* static, paywalled or PDF, publication-only,
  not funder/trial/advocacy maps, not maintained, not family-facing, not reusable data.

---

## 3. Gaps we can fill

1. **One open, source-linked, Ewing-specific cross-ecosystem map** uniting funders + grants + orgs +
   trials + outputs + advocacy groups — no existing free tool spans all of these for Ewing.
2. **Assertion-level provenance** (every fact resolves to a specific open record) — World RePORT,
   foundation pages, and bibliometric reviews don't offer this.
3. **Openly-licensed reusable dataset (CSV + JSON-LD, persistent IDs)** that families, small
   foundations, and researchers can *download and reshape* — the integrated commercial views forbid
   exactly this.
4. **Family/advocate-oriented, non-clinical orientation layer** ("who is working on this, where is
   the money going") — a register that World RePORT/Dimensions/Candid are not designed for and don't
   serve.
5. **An honest "known gaps" ledger** — no competitor publishes what it *misses*; this is a structural
   differentiator for a trust-first tool.
6. **The long tail of small family foundations** consolidated and reconciled — Candid paywalls it,
   990s under-describe it, and it lives in scattered HTML today.
7. **Reconciliation to the open identifier web (ROR/ORCID/Funder Registry/NCT/DOI)** so the map is
   interoperable with Wikidata/OpenAlex from day one — foundation listings and World RePORT are not.

---

## 4. Differentiators to win

- **Open + reusable + cited, not paywalled or screen-only.** The only player that is simultaneously
  free, openly licensed for redistribution, *and* integrated across funders/grants/trials for Ewing.
- **Provenance-on-every-assertion + published gaps ledger = auditable trust.** Honesty about blind
  spots is a feature no competitor offers and the one families/advocates most need.
- **Neutral by construction (no ranking field in the schema).** Structurally cannot become a
  "best lab" scorecard — a credibility moat for an advocacy-adjacent tool.
- **Disease-specific curation with a published, reproducible inclusion query.** Generic tools
  (World RePORT, OpenAlex) can't tell you "this is the Ewing slice, and here's exactly how we drew
  the boundary."
- **Family-first framing held with discipline** (orientation, never advice; advocate-reviewed). This
  is a use-case the commercial research-intelligence stack actively ignores.
- **Persistent IDs decoupled from any host** (w3id.org PURL) — survives steward changes, so the map
  is never orphaned; a durability promise advocacy orgs can rely on.

---

## 5. Claude API leverage

**Where Claude clearly helps (assistive, human-verified):**

1. **Entity extraction & normalization from messy open records** — turn free-text RePORTER abstracts,
   CORDIS summaries, AACT sponsor fields, and especially *unstructured foundation HTML grant pages*
   into typed Org/Grant/Effort candidates with field-level confidence and a "flag-on-doubt" output.
   This directly attacks the long-tail-foundation gap that has no structured source.
2. **Reconciliation candidate generation & disambiguation triage** — propose ROR/ORCID/Funder
   Registry matches with reasoning ("same org, name variant + country + ROR alias") for a human to
   confirm; cluster likely-duplicate efforts and explain *why*, raising reviewer throughput without
   auto-merging.
3. **Plain-language, sourced org/effort profiles** — generate neutral, non-clinical one-paragraph
   "what this foundation/lab/consortium publicly does" blurbs, each sentence tied to a cited record,
   for the family/advocate layer.
4. **Inclusion-query assistance & gap narration** — help expand MeSH/keyword/synonym seeds
   (EWSR1, FLI1/ETS, Askin/PNET historical terms) and draft *descriptive* gaps-ledger entries.
5. **Anti-laundering / anomaly spot-checking** — flag records bearing tell-tale proprietary-DB
   artifacts, or outlier amounts/dates, for human review.
6. **Multilingual ingestion** — read non-English national-charity/funder pages (DFG, INCa, NHMRC) to
   widen international coverage — directly addressing the US/EU-skew gap.

**Where Claude must NOT decide (hard limits, enforced by the plan's gates):**

- **No value judgments** — never label a lab/funder/region "best," "leading," "neglected," or
  "under-funded" as fact; gap language stays descriptive and human-approved. (No-ranking rule.)
- **No fabricated affiliations, amounts, links, or IDs** — if a field isn't in the cited record, it
  stays empty and flagged; gaps stay gaps (no inference fill).
- **No autonomous reconciliation/merges** — every ROR/ORCID/effort merge is human-confirmed and
  reversible; zero-false-merge bar.
- **Accuracy is human-verified** — Claude output enters the same stratified ≥95% citation audit;
  amount/currency assertions get the strictest scrutiny.
- **Neutrality is human-reviewed** — all family-facing and gaps text passes patient-advocate review;
  "not medical advice" preserved.
- **Individual-researcher privacy respected** — only public professional facts; Claude never infers
  or assembles dossiers; honors the correction/removal process.
- **License calls are human-verified** — Claude may *summarize* a source's terms but never *approve*
  a source; the named license reviewer decides `approved`.

---

## 6. Ten concrete optimizations

1. **Add World RePORT** as both a benchmarked competitor and a reconciliation/coverage cross-check
   source (it already maps 6 major funders internationally).
2. **Split "foundation grants" intake from 990s**: add a dedicated, license-checked
   foundation-public-listing extractor (QuadW, SFA, St. Baldrick's, AACR) using Claude HTML
   extraction; treat 990s as a *secondary corroboration*, not the primary foundation source.
3. **Add a coverage/recall metric against a known frame** (e.g., "% of all ClinicalTrials.gov
   records matching the published Ewing query that are captured"), so the *gaps* tool can quantify
   its own completeness — not just absolute counts.
4. **Specify a PI-matching precision policy** (ORCID-anchored; name-only matches left unmerged;
   stated false-merge tolerance) mirroring the ROR blocking-key rigor.
5. **Pin the currency-normalization date rule** (award-start vs. fiscal-year tranche) and document
   multi-year handling, with worked examples in the data dictionary.
6. **Make freshness SLAs per-source-cadence** (e.g., AACT daily, RePORTER weekly, CORDIS/GtR monthly,
   990s annual-with-lag) instead of one global "90% within 90 days."
7. **Adopt a neutrality rubric for the gaps ledger and explorer copy** — descriptive, non-evaluative
   language only; add it to the patient-advocate + accuracy review checklist; audit for
   ClinicalTrials.gov "no implied endorsement."
8. **Add an inclusion/appeal path** symmetric to removal: a small foundation can request to be
   considered against the published query (selection transparency cuts both ways).
9. **Lean harder on OpenAlex's funder/grant graph (CC0)** as a discovery + cross-funder source to
   partially replace what Dimensions paywalls, and to bootstrap international coverage.
10. **Define a "partial-win" success threshold** if no steward signs (e.g., dataset deposited in a
    public repository with a DOI + ≥1 external citation/reuse), so public good is captured even when
    "shipped" isn't met.

---

## 7. Parallel & perpendicular spin-offs

- **`ewing-trial-finder` (feeds from this map).** This project's reconciled NCT records + sponsor↔ROR
  links become the trusted backbone; the high-risk plain-language/eligibility interpretation lives
  there behind oncologist + advocate review. Clean feed: aggregate StudyRecords here → clinical layer
  there.
- **`ewing-outcomes-harmonization`.** A standards/crosswalk effort aligning how Ewing outcomes are
  reported across registries/trials — consumes this map's trial+output graph as its index. (Stays
  out of patient data; harmonizes *definitions/metadata*, not records.)
- **`open-spending-explainers`.** Plain-language, neutral "where did this funder's Ewing money go"
  narratives built strictly on this map's grant+provenance layer — a natural reuse of the family
  orientation layer + Claude summarization, advocate-reviewed.
- **Generalized rare-disease research-landscape engine.** The pipeline (allow-list gate → inclusion
  query → extract → provenance bind → reconcile → gaps ledger) is disease-agnostic. Re-parameterize
  the inclusion query and seed list to spin up DIPG, neuroblastoma, rhabdomyosarcoma, or any rare
  cancer/disease map — the highest-leverage perpendicular play.
- **MCP server ("rare-disease research map").** Expose the reconciled, source-linked graph as an
  read-only [MCP](https://modelcontextprotocol.io) server so any agent can answer "who funds Ewing
  research, with citations" — turning the dataset into queryable, provenance-carrying tooling for the
  open-science agent ecosystem.
- **Wikidata round-trip (already a backlog item).** Push reconciled ROR/ORCID/Funder/NCT links back
  to CC0 Wikidata — strengthens the commons and creates a durable, host-independent home for the
  graph.

---

## 8. Open questions for the maintainer

1. **Why is World RePORT absent from the plan**, and will it be added as competitor + source +
   coverage cross-check before M2?
2. **What is the v1 international strategy?** Is a US/EU-only first release acceptable given the
   disease's international fragmentation, or should ≥1 non-US/EU national funder be a v1 gate?
3. **How are small family foundations actually ingested** if 990s under-describe them and their grant
   pages are unstructured HTML — is a dedicated foundation-page extractor in scope for M2 vs. backlog?
4. **What is the PI-disambiguation precision rule and target** (parallel to the 85% ROR target)?
5. **Which date anchors FX normalization** for multi-year, multi-tranche awards?
6. **What is the neutrality rubric for the gaps ledger** so "gap/under-funded" language doesn't read
   as criticism/endorsement, and who signs off on it?
7. **Default disposition of a disputed living-investigator record during review** — hidden or shown?
   And will a recorded GDPR/UK-GDPR legitimate-interest assessment back the EU/UK PI data?
8. **Is re-enclosure of the CC-BY dataset by a proprietary product acceptable**, or should a
   ShareAlike/anti-enclosure stance be considered for the *compiled* data?
9. **What is the "partial win" definition** if no steward is ever secured?
10. **How is overlap with `ewing-open-data-catalog` / the KG operationalized** to avoid two divergent
    Elyos maps of the same orgs?
