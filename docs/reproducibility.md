# Reproducibility checklist

Completion is per dataset and result, not a single claim that the project is
reproducible. Recovery checks and scientific validation are separate.

## Inputs and evidence

- [x] Preserve recovered working files unchanged and record paths, byte counts,
  SHA-256 and source-artifact metadata in `recovery_manifest.csv`.
- [x] Identify the four CSV byte streams matching the historical Bondetti v1.0 freeze.
- [ ] Verify source publications, supplements, citations, licences and exact
  table/page/row locators; retain retrieval dates and original-file hashes.
- [ ] Compare transcriptions against those sources, including rounding,
  inequalities, missingness, replicate identity and negative observations.
- [ ] Reconcile the network snapshots and establish which files belong together.
  Do not use the reported v0.3 counts as a completeness test for later files.
- [ ] Resolve the integration-manifest mismatches and recover missing builders.
- [ ] Populate the reviewed tables and audit the provenance links described in
  `provenance.md`. Record contrary evidence and unresolved assignments.

## Transformations and analysis

- [ ] Specify every inclusion/exclusion, join, unit conversion, digitisation,
  denominator, normalisation, zero replacement, imputation and aggregation.
  Retain the untransformed values and a mapping to each input row.
- [ ] Distinguish a reported absence from an unmeasured/unreported quantity.
- [ ] Review the recovered statistical code, including compositional distances,
  mixture constraints, fitting/prediction separation and any parameter search.
- [ ] Specify sensitivity checks, replicate limitations and what cannot be
  inferred without absolute yields or additional controls. Avoid treating
  repeated citations or derived measures as independent observations.
- [ ] Record random seeds, sample splits, model parameters, numerical tolerances
  and uncertainty calculations wherever applicable.

## Software and reruns

- [x] Provide a standard-library check of imported file integrity.
- [x] Provide a helper that stages exact copies for the recovered data-QA script.
- [ ] Before a scientific run, record OS, Python and exact direct/transitive
  package versions; establish a tested installation/lock file for that analysis.
  `requirements-qa.txt` pins direct QA dependencies only, not the full analysis.
- [ ] Reproduce the analysis from a fresh checkout/environment using only
  declared inputs. Remove dependence on personal absolute paths and old outputs
  in a reviewed copy of the historical code.
- [ ] Confirm the run stops for missing inputs or failed checks. Verify each
  output against the expected values/tolerances; investigate failures.

## Versioned outputs and paper

- [ ] Store an accepted run in a new `results/<date>-<short-label>/` directory.
  Include the source commit, input hashes, commands in order, package versions,
  parameters/seeds, exit statuses, logs, output hashes and known limitations.
- [ ] Record the distinction between a successful execution, a reproduced old
  numerical result, and a source-validated scientific conclusion.
- [ ] Generate each final figure from those outputs; record script/command,
  input/run ID, caption, units and any manual edits. Keep editable source.
- [ ] Update methods, limitations, data availability and rights statements.
- [ ] Assign a dataset/result version and Git tag only after review. Corrections
  require a new version with an explanation; do not overwrite a released result.

The dated recovery QA report records what was actually run during setup. Its
success does not tick the scientific-analysis or primary-source checks above.
