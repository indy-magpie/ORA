# Recovery record — 24 October 2026

## What was checked

The GitHub API reported an empty `indy-magpie/ORA` repository with no branches
before initialization. Earlier conversations supplied discovery leads, not
scientific evidence. Targeted searches of existing project files then recovered
the byte streams listed in `recovery_manifest.csv`. Broad content search missed
files which exact/partial filename searches found; absence from these searches
is not proof that an artifact no longer exists elsewhere.

**38 original artifacts are preserved:** 18 Bondetti files, 11 network files,
8 integration files and 1 reference workbook. Original names and bytes are
retained. Five byte-identical alternate filenames were deduplicated and recorded
as aliases in the inventory. Source creation timestamps are file metadata,
not proof of a scientific version or date of analysis. The original environment
and authorship/verification history of every artifact are not established.

## Bondetti dataset freeze recovered

The historical `README-2.md` describes a published-data reanalysis and
`MANIFEST.v1.0.txt` records a freeze dated 11 August 2026. All four expected
SHA-256 hashes match recovered files:

| Expected filename in the freeze | Recovered filename | Data rows |
| --- | --- | ---: |
| `bondetti2021_field_samples.csv` | same | 51 |
| `bondetti2021_isomers_long.csv` | same | 657 |
| `bondetti2021_precursor_ufa.csv` | same | 39 |
| `bondetti2021_treatments.csv` | `bondetti2021_treatments-1.csv` | 75 |

These counts describe CSV records, not independent experimental replicates.
The unsuffixed treatments file has 59 rows; `treatments(1).csv` has 75 rows but
a different hash. Both are retained as historical alternatives. The QA helper
uses the hash-matched `-1` version and renames only its temporary copy.

The 00–06 analysis scripts, their loader and an alternative script 03 were
recovered. The old filename `00_data_QA-1.py` is the manifest-checking QA version;
the helper stages it as `00_data_QA.py`. No historical analysis was reimplemented.
The original scientific environment and selection of script 03 remain unresolved.

The supported QA execution returned **29 checks: 28 PASS, 0 FAIL, 1 WARN**.
The warning concerns four precursor rows outside the script's 100 ± 1 percentage
point closure check; the recovered values span 91.7–100.1. This is a property of
the recovered table, not a fresh finding about the publication. The old warning
message labels the minimum-sum row but prints the maximum when any sum exceeds
100; its inconsistent “worst” phrase is preserved in the log, not endorsed.
Do not edit the historical script to conceal this reporting defect.

See `results/2026-10-24-recovery-qa/` for the exact QA report, log, environment,
staging map and hashes. No statistical reanalysis or source-by-source
transcription check was run.

## Network version boundaries

The user's historical v0.3 description is **25 compounds / 23 reactions /
30 evidence records**. No matching complete snapshot was recovered. The table
counts actually observed are:

| Original filename | Data rows |
| --- | ---: |
| `compounds.csv` / `compounds-1.csv` | 21 / 37 |
| `reactions.csv` / `reactions-1.csv` | 20 / 32 |
| `reaction_evidence.csv` / `reaction_evidence-1.csv` / `reaction_evidence-2.csv` | 27 / 53 / 57 |
| `isomer_assignments.csv` / `isomer_assignments-1.csv` | 9 / 9 |

These are **separate recovered files**, not a newly assembled network of
37 compounds, 32 reactions and 57 evidence rows. Matching names, timestamps or
suffixes do not establish a coherent release. `README-4.md` labels itself v0.7;
the later integration manifest refers to v0.8 but does not hash the core network
tables. The full version mapping and the historical `build_network.py` and
`qa_network.py` were not recovered.

The old v0.7 README retains earlier sections contradicted by its own later
corrections: for example, its “Six structural gaps” section says no intermediate
was isolated, whereas the v0.4 account says one was. This is a documented
conflict **inside project notes**, not a new adjudication of the chemistry.
`destaillats_integration_notes.md` contains later proposed changes and unresolved
distinctions between ring formation and aromatisation. Neither document is
promoted to verified current conclusions.

## Integration freeze is incomplete

`recovered/integration/MANIFEST.txt` describes an
`experimental-integration-v1` freeze and network state v0.8. Of its 12 expected
files, **3 match, 3 differ and 6 were not imported/recovered**:

| Status | Files |
| --- | --- |
| Hash match | `phd_material_experiments.csv` (15 rows), `phd_actualistic_experiments.csv` (6 rows), `precursor_mechanism_matrix-1.csv` (6 rows; original manifest expects the unsuffixed name). |
| Hash mismatch | `09_experimental_bridge.py`, `claims.csv` (34 rows), `materials.csv` (4 rows). |
| Missing from this recovery | `build_claims.py`, `build_figure.py`, `build_phd_experiments.py`, `build_precursor_matrix.py`, `figure_network.pdf`, `figure_network.png`. |

The byte-level comparisons are in `freeze_comparison.csv`. A mismatch does not
identify which file is correct or why it changed. Do not rewrite the historical
manifest to make it agree with the recovered files. The matrix's unsuffixed
alternative also differs and is retained separately.

The manifest carries an unresolved feedstock-charge query (“approximately
65 mL” of oil against 4 g of matrix). Its resolution and underlying thesis
passage were not recovered or verified here. Preserve the stated value and flag;
do not silently convert it to a more plausible quantity. Keep the laboratory
and actualistic experiments separate as the original records intended.

## Literature and remaining inputs

`APAA_reference_corpus.xlsx` is retained unchanged. Its opening instructions
explicitly warn that some entries are “Reconstructed” or “Placeholder” and need
bibliographic verification. It is a recovery aid, not a verified reference list.
The Bondetti main-paper PDF was also located but is not redistributed. The
source supplements and full primary mechanistic corpus were not verified in
this task. No citation was constructed from memory or promoted from a notebook
without source checking.

The next scientific work is to recover/verify those sources, resolve the
integration differences and network version membership, and migrate checked
observations using `provenance.md`. Empty current tables label that work honestly;
they do not imply the historical data are absent. A future result must link to
the exact source commit, input hashes, transformation steps and environment.
