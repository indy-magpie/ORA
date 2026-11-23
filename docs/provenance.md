# Minimal provenance convention

## One claim, an explicit route to its source

Use five small CSV tables. The templates are empty pending review. Prefixes are
namespaces, not confidence scores; assign stable zero-padded identifiers from
`0001` upward. Do not recycle an identifier after deletion.

| Table / ID | Unit of record | Required links |
| --- | --- | --- |
| `references.csv` / `REF-0001` | One actual publication, dataset, thesis or dated project note | Verified bibliographic identity or a clearly labelled project-file path. |
| `compounds.csv` / `CMP-0001` | One specified chemical identity, explicitly unresolved isomer or compound class | Evidence rows for any identity claim; retain structural uncertainty. |
| `reactions.csv` / `RXN-0001` | One proposed transformation | `reactant_ids` and `product_ids` resolve to CMP records. |
| `observations.csv` / `OBS-0001` | One reported measurement/outcome for an experimental unit and target | One REF, an exact source locator, experiment/sample identifier and CMP where applicable. |
| `evidence.csv` / `EVD-0001` | One explicit evidential statement about a CMP or RXN | `subject_id` resolves to CMP/RXN; one REF; an OBS for a reported experimental observation. |

These ID strings illustrate format only; they are **not populated scientific
records**. `source_locator` means page + table/figure/scheme + row, cell, panel
or passage as appropriate. A DOI alone is not a measurement locator.

An observation links to its literature reference. An evidence row links that
observation to a compound identity or reaction proposition. Multiple studies
supporting one reaction require separate evidence rows. Repeated citations of
one experiment retain the same observation identity and must not be counted as
independent experiments.

## Meanings and controlled values

| Field | Allowed values / interpretation |
| --- | --- |
| Reference `source_kind` | `primary_paper`, `review`, `thesis`, `dataset`, `project_note`. |
| Reference `access_status` | `read_directly`, `read_via_citation`, `metadata_only`, `not_accessed`; this reports access, not correctness. |
| Compound `entity_type` | `defined_structure`, `unresolved_isomer`, `compound_class`. Do not put a generic class under a falsely precise SMILES. |
| Compound `identity_status` | `reported_assignment`, `tentative_assignment`, `unresolved`, `project_hypothesis`. Evidence supplies the basis. |
| Reaction `mechanism_status` | `proposed`, `supported`, `disputed`, `superseded`. `supported` is limited to the cited conditions, never automatic proof of the full pathway. |
| Observation `observation_status` | `reported`, `not_detected`, `below_quantification`, `not_reported`, `not_applicable`, `uncertain`. Non-detection is conditional on method/sensitivity. |
| Evidence `relation` | `supports`, `contradicts`, `context_only`. |
| Evidence `assertion_type` | `reported_observation`, `author_interpretation`, `project_hypothesis`. Do not recast an author's scheme as an observed intermediate. |
| Evidence `access_basis` | `direct_source`, `secondary_citation`, `project_record`. A recovered note's old `READ_DIRECTLY` label alone does not establish direct access in the new table. |
| Observation/evidence `review_status` | `unreviewed`, `source_checked`, `disputed`, `superseded`. `source_checked` means checked at the stated locator, not scientifically proven. |
| Observation `extraction_method` | `transcribed`, `digitised`, `source_file`, `legacy_import`; document the procedure and any calculation in `notes`. |

`reference_id`, `subject_id` and `observation_id` are single foreign keys.
For a reaction with several participants use semicolon-separated CMP IDs in
the participant columns; order has no stoichiometric meaning. Do not imply
stoichiometry or mass balance from this simple edge table.

For a project hypothesis use an actual dated project note as the REF and
`project_record` as the access basis. Leave OBS blank when no experimental
observation is asserted. For a secondary citation, REF identifies the document
actually read; identify the attributed primary source in `notes`, record its
access status separately, and do not claim to have read it.

## Conditions, identity and missingness

Record the experimental unit and distinguish technical replicates, independent
preparations and repeated readings. A source-specific `experiment_id` is scoped
by REF. Conditions include feedstock, temperature, time, atmosphere, matrix or
catalyst and any staged treatment/workup; document missing conditions explicitly.
Do not collapse closed laboratory treatments and actualistic samples into one
condition merely because both were heated.

`reported_value` preserves the source representation, including inequalities and
qualifiers; `reported_unit` preserves its units. If the source uses another unit
than a condition column requires, record the original and conversion in notes.
Blank means unknown/absent, never zero. Explain missing conditions, identities
and values in notes; use `observation_status` for outcome missingness. A measured
zero must be explicit and distinguishable from a non-detection. Do not overwrite
source percentages with closed compositions, imputed zeros or fitted weights.
Derived tables belong in a versioned result directory with a transformation log.

State chain length, substitution, stereochemistry and identification limits
when available. Isomer letters are scoped to paper and analytical method;
identical letters across studies are not proof of identical structures. Preserve
the recovered isomer-assignment tables while their alignment is reviewed.

## From historical files to reviewed rows

Never edit `recovered/`. Keep its original IDs and spellings intact. For a new
row set `legacy_locator` to a repository-relative path plus original key; if no
key exists, use the 1-based data-row ordinal, explicitly excluding the header.
The path resolves through `docs/recovery_manifest.csv` to a SHA-256. This prevents
the same legacy ID from different snapshots being merged by accident.

Record any spelling, structural, value, unit or interpretation change with the
source locator, reason and review date in the migration commit and row notes.
Split observations from interpretations; do not import historical confidence
labels as newly verified evidence. Add a new record for a materially different
identity or experiment. Mark superseded assertions and explain their successors.

Before accepting a table: check unique IDs; all foreign keys and participant IDs;
source locators; the controlled values; unresolved identity/units; duplicate
experiments; and that every `reported_observation` evidence row has an OBS link.
These semantic checks are manual at this scaffold stage. The recovery verifier
does not perform them.
