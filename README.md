# ewing-research-landscape

> There is no open, queryable, source-linked map of the Ewing Sarcoma research landscape. The information exists — in NIH RePORTER, the EU's CORDIS, UKRI's Gateway to Research, the trial registries, Ope  ·  **Risk tier:** low  ·  **Status:** planning

There is no open, queryable, source-linked map of the Ewing Sarcoma research landscape. The information exists — in NIH RePORTER, the EU's CORDIS, UKRI's Gateway to Research, the trial registries, OpenAlex, ROR, and the public filings of dozens of small Ewing/sarcoma foundations — but it is **scattered across a dozen systems, in incompatible formats, with no shared identifiers, and no provenance a family or advocate could check.** The richest *integrated* views of this landscape (Dimensions, Web of Science, Scopus, Candid/Foundation Directory) are **proprietary research-intelligence products behind license terms that forbid redistribution** — exactly the people who most need the picture (families, patient advocates, small foundations, early-career researchers) cannot get it.

**Definition of shipped:** research ecosystem with: **100%** provenance on assertions; ≥4 integrated open sources; canonical-ID reconciliation at target coverage; original currency/amount retained on 100% of grants; a current **"known gaps" ledger**; passing CI (schema + provenance + allow-list + freshness

This is an **Elyos** good-deed project. Contributors pull a task, do it with their own coding agent, and open a PR. Platform: https://github.com/jdev1977/elyos

## Plan
- [PLAN.md](./PLAN.md) — robust enterprise plan (vision, architecture, roadmap, risks; includes an applied-improvements appendix + review sign-off)
- [TASKS.md](./TASKS.md) — schema-mapped task backlog
- [tasks/](./tasks/) — ready-to-pull task JSON(s)

## Contribute
```bash
elyos browse
elyos next --repo Elyos-Projects/ewing-research-landscape --no-fork
```

## Licensing & review
- Open license (see PLAN.md).
- Risk tier **low** — deeds are *delivered, not merged*; standard review applies.

> Planning stage; no adopting partner secured yet (`verifiedNeed: false` on delivery-dependent tasks).
