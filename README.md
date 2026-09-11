# cloud-itonami-lei-wp5o65e6bmu84lno4227

> **Independent third-party archive/analysis. Not affiliated with, endorsed by, or sponsored by Sirius XM Radio LLC.**

This repository archives publicly published legal/policy documents of
**Sirius XM Radio LLC**, with source-url and retrieval-date provenance, per
[ADR-2607110300](https://github.com/com-junkawasaki/root/blob/main/90-docs/adr/2607110300-cloud-itonami-lei-corporate-tos-catalog.md)
(`cloud-itonami-lei-corporate-tos-catalog`, `com-junkawasaki/root`). It is a read-only
reference/archive repository — it does not act, propose, or execute anything on the
company's behalf, and is not a governed Advisor/Governor actor.

## Company identity

- **Legal name**: Sirius XM Radio LLC — exactly the live GLEIF record's spelling
  (language `en`, last updated 2025-09-04). The same record lists two
  `PREVIOUS_LEGAL_NAME` entries, `Sirius Satellite Radio Inc.` and `CD Radio Inc.`
  (read from `otherNames` of the cited LEI record URL on 2026-08-23); the vendored
  checker does not emit `otherNames`, so those two names are cited here but are
  **not** gated by `facts.edn`.
- **LEI (ISO 17442)**: [WP5O65E6BMU84LNO4227](https://search.gleif.org/#/record/WP5O65E6BMU84LNO4227) (GLEIF-verified)
- **Jurisdiction**: US-DE — registered with the Delaware Division of Corporations,
  Department of State (`RA000602`, file number `2230857`, OpenCorporates
  `us_de/2230857`), created 1990-05-17; legal address c/o The Corporation
  Trust Company, 1209 Orange Street, Wilmington, DE 19801, and
  headquarters at 1221 Avenue of the Americas, New York, NY 10020.
- **Website**: https://www.siriusxm.com
- **Securities**: GLEIF maps **20 ISINs** to this LEI (two pages of 15 at the cited
  URL). They are counted, not mirrored, in `facts.edn`: at this volume the list turns
  over as instruments mature and are issued, which would make the check red for a
  reason that is not "the citation broke". What kind of instruments they are, and
  whether any is admitted to trading, is not something GLEIF answers, so no ticker
  is asserted here.

## Contents

- `80-data/public/tos.journal.edn` — EDN quad-log of archived documents, each entry
  carrying `:tos/full-text`, `:tos/source-url`, `:tos/retrieved-at`, `:tos/sha256`,
  `:tos/doc-type`, and a `:tos/supersedes` chain for future revisions.
- `NOTICE` — copyright/attribution statement for the archived third-party text.
- `blueprint.edn` — machine-readable company identity record.
- `facts.edn` — 9 verified registry facts with per-fact provenance (the entity, its
  securities count, issuer and issuer accreditation, registration authority, legal
  form, both parent-reporting exceptions, and the direct-children count).
  **Generated** — see below.
- `scripts/verify-facts.cljk` — re-fetches every source `facts.edn` cites and fails if
  the live record disagrees. Vendored from `com-junkawasaki/root`
  (`scripts/lei-verify-facts.cljs`); fix issues in the canonical and re-vendor.

## Verifying the record

The LEI claims above used to be assertions with nothing in the repository behind
them. `facts.edn` now carries them as data, and every value in it was read out of a
public registry response whose URL and retrieval time sit next to the value:

```
kbb --backend sci scripts/verify-facts.cljk           # check the recorded facts against the live sources
kbb --backend sci scripts/verify-facts.cljk --write   # re-fetch and rewrite facts.edn
```

Eleven GLEIF/ISO requests back the file (`CHECKED 11` when it was written,
2026-08-23T08:38Z, golden copy 2026-08-23T00:00Z) — the LEI record (legal name
`Sirius XM Radio LLC`, jurisdiction `US-DE`, entity category `GENERAL`, entity
**ACTIVE**, registration **ISSUED** since 2012-06-06 with the next renewal due
2026-09-11, last updated 2025-09-04, `FULLY_CORROBORATED`, conformity flag
**`NON_CONFORMING`** — GLEIF's own data-quality flag on the record, which is a
separate field from both the entity status and the corroboration level and is
recorded as the registry states it; the API response does not say which check
fails, so no cause is asserted here — no BIC, S&P Global id `248607529`,
OpenCorporates `us_de/2230857`; entity status and registration status are
different fields and are recorded separately), its **20 ISINs** as a count read
from `meta.pagination.total` of the cited page, its managing LOU and LEI-issuer
accreditation (Bloomberg Finance L.P., LEI `5493001KJTIIGC8Y1R12`, accredited
2017-04-13), registration authority `RA000602` (Division of Corporations,
Department of State, Delaware), ISO 20275 legal form `HZEH` (`Limited Liability
Company`, `US-DE`), reporting exceptions at both consolidation levels (`NO_LEI` —
GLEIF's reason code for a level whose consolidating parent holds no LEI, so the
registry names no parent at either level; this file records that answer, not a
group chart, and nothing about who owns this entity is asserted here), and a
measured **0 direct children**, read from `meta.pagination.total` of the cited
page. The `direct-parent` and `ultimate-parent` endpoints answered `404` because
GLEIF publishes the exception side of that pair for this entity, which the checker
treats as a fact rather than a failure.

The checker's exit codes are three, not two: `0` every recorded fact matches the
live sources, `1` a citation broke or a fact drifted, `3` the check could not be
performed at all — an absent `facts.edn`, or every request failing at the
transport level. A check that could not run must not be indistinguishable from a
check that ran and found nothing, so it refuses to report a pass rather than
exiting 0. All outcomes were exercised before this landed: unmodified `0`
(`OK all 9 recorded fact(s) still match`); `:securities/isin-count` edited
`20` → `21` → `1` naming `DRIFT gleif-isins :securities/isin-count`;
`:company/legal-name` rewritten to `Sirius XM Radio Inc.` → `1` naming
`DRIFT gleif-lei-record :company/legal-name`; the measured
`:relationship/direct-child-count` rewritten `0` → `1` → `1` naming
`DRIFT gleif-direct-children-count`; the direct-level
`:relationship/exception-reason` rewritten to `NON_CONSOLIDATING` → `1` naming
`DRIFT gleif-direct-parent-reporting-exception :relationship/exception-reason`;
file number `2230857` rewritten `2230858` → `1` naming the drift in
`gleif-lei-record` (`:company/registered-as` and `:company/open-corporates-id`)
and `gleif-registration-authority`; `:registration/conformity-flag` rewritten to
`CONFORMING` → `1` naming `DRIFT gleif-lei-record :registration/conformity-flag`;
`:elf/local-name` rewritten → `1` naming
`DRIFT iso-20275-entity-legal-form :elf/local-name`; the GLEIF host in the checker
rewritten to an unresolvable name → `3` (`INCONCLUSIVE … refusing to report a
pass`); and with no `facts.edn` at all → `3` (`INCONCLUSIVE facts.edn is missing
or holds no facts`). Each mutation was reverted and the restored file compared
byte-for-byte against the generated one.

`facts.edn` is not yet on the shared query plane: `manifest/edn-query.cljs` in
`com-junkawasaki/root` has loaders for `blueprint.edn` and the ToS journal and none
for this file, so its datoms load here but are not joinable from `edn-query`.

## Design rationale

See ADR-2607110300 in `com-junkawasaki/root` (`90-docs/adr/`) for why this repo exists,
why it is keyed by LEI rather than GTIN or ticker, and why full-text archival (with
provenance) was chosen over excerpt-only storage.
