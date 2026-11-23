# ORA — APAA formation and interpretation

A small computational archaeology project examining ω-(o-alkylphenyl)alkanoic
acids (APAAs), their formation chemistry, and what published experimental
observations can support in archaeological organic residue analysis.

## Project status — 24 October 2026

This is a **reproducibility scaffold and recovery of historical working files**,
not a completed analysis or a validated reaction mechanism. The repository was
empty when inspected for this task. Its contents now distinguish:

- **Recovered artifacts:** unchanged project files with recorded SHA-256 hashes.
  The four Bondetti reanalysis CSVs match the recovered v1.0 freeze manifest.
- **Historical interpretation:** scripts, network tables and notes retained in
  `recovered/`. Their claims and `READ_DIRECTLY` labels have not been reverified
  against the literature during this recovery.
- **Reviewed evidence:** the five tables under `data/` currently contain headers
  only. Populating them requires source checking and explicit provenance.
- **New results:** no scientific results have been reproduced or accepted here.
  Any recovery/QA report under `results/` concerns file integrity and internal
  data consistency only.

The previously described **v0.3: 25 compounds, 23 reactions, 30 evidence records**
is a historical description, not a count of a recovered, verified release.
Later notes mention v0.7 and v0.8. The accessible tables cannot yet be assigned
as complete snapshots of those versions. See [the recovery record](docs/recovery.md)
for exact counts, hash comparisons and unresolved inputs.

## Research questions

1. Which proposed APAA formation steps are supported by direct observations,
   and which rest on product distributions, literature attribution or project
   hypotheses?
2. How do precursor composition, temperature, duration, atmosphere, preparation
   and matrix/catalyst conditions relate to the reported products?
3. What do reanalyses of published compositional data establish, and how
   sensitive are those conclusions to missingness, zero handling,
   normalisation, model assumptions and small replicate numbers?
4. Where does evidence from laboratory treatments transfer to archaeological
   interpretation, and where does that transfer remain untested?

These are questions to investigate, not findings. APAA observations, proposed
formation mechanisms and biological-source attribution are separate claims.

## Analytical approach and intended outputs

Recover and preserve the existing files; verify the primary publications and
supplements; extract observations with table/page/row locators; then link them
to compounds and reaction hypotheses. Keep reported measurements separate
from authors' interpretations and this project's inferences.

The recovered Bondetti scripts provide a starting point for compositional
reanalysis, mixture comparisons and sensitivity checks. Review their assumptions
and dependencies before adopting a current analysis. Relative profiles must not
be silently reinterpreted as absolute yields. A network edge is a proposition
with evidence, not proof that a pathway operates in a cooking vessel.

Intended paper outputs are a source-linked evidence table, a qualified reaction
network, reproducible reanalysis tables and figures, and a short methods and
limitations account. No new experiments or missing scripts are fabricated.

## Repository layout

| Location | Purpose |
| --- | --- |
| [`recovered/`](recovered/README.md) | Unchanged historical data, code, notes and reference corpus; preserve original names. |
| [`data/literature/`](docs/provenance.md) | References, extracted observations and evidence links; header-only pending review. |
| [`data/network/`](docs/provenance.md) | Compounds and reaction hypotheses; header-only pending version reconciliation. |
| [`data/raw/`](data/raw/README.md) | Future primary-source supplements; recovered transcriptions already live in `recovered/`. |
| [`analysis/`](analysis/README.md) | Plan for a reviewed analysis and instructions for the recovered code. |
| [`scripts/`](scripts/) | Small recovery verification and historical QA launch helpers. |
| [`figures/`](figures/README.md) | Versioned paper figures with generating command and result provenance. |
| [`results/`](results/README.md) | Labelled, versioned run records; no accepted scientific results yet. |
| [`docs/`](docs/) | Provenance convention, recovery inventory and reproducibility checklist. |
| `work/` | Ignored disposable execution area; created by the QA helper. |

## Start here

From the repository root, with Python 3.10 or newer:

```sh
python scripts/verify_recovery.py
```

This uses only the standard library and verifies the imported bytes against
`docs/recovery_manifest.csv`. It does **not** check the underlying science.

To rerun the recovered Bondetti **data QA only**, use a separate environment
(tested here with Python 3.12.14):

```sh
python -m venv .venv
# POSIX: source .venv/bin/activate
# PowerShell: .\.venv\Scripts\Activate.ps1
python -m pip install -r requirements-qa.txt
python scripts/run_recovered_qa.py
```

The helper checks the recovery inventory, stages exact copies and the original
freeze manifest in a fresh directory under `work/`, and runs the recovered QA
script. It prints that directory and leaves the originals untouched. The pinned
packages describe the QA environment tested during recovery, not the unknown
historical environment or a validated scientific analysis environment.

Before adding evidence or interpreting outputs, read
[the provenance convention](docs/provenance.md) and
[the reproducibility checklist](docs/reproducibility.md).

## Scope and reuse

Keep this as files, CSV tables and small scripts. A database, workflow platform
or new statistical implementation is not needed for this initial scaffold.
No project-wide licence has been selected. Retained third-party citations and
source materials keep their own rights; verify redistribution terms before
adding publication PDFs or supplements. The source PDF located during recovery
has not been copied into this public repository.
