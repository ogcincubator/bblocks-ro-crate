## Provenance

Converted from the Bioschemas [ComputationalWorkflow 1.0-RELEASE](https://bioschemas.org/profiles/ComputationalWorkflow/1.0-RELEASE)
profile's `$validation` block (JSON Schema draft-07), as published in
[`BioSchemas/specifications`](https://github.com/BioSchemas/specifications/tree/main/ComputationalWorkflow).
This is the profile RO-Crate's [Workflow RO-Crate](https://www.researchobject.org/ro-crate/specification/1.3/workflows.html)
specification points to for describing a crate's Main Entity.

## Deviations from the source profile

- The source's non-standard `owl:cardinality` annotations and top-level `required`/`recommended`/
  `optional` triage are dropped in favor of plain JSON Schema `required`, matching the profile's
  own `required` list (`input`, `output`, `programmingLanguage`, `name`, `url`, `creator`,
  `dateCreated`, `license`, `sdPublisher`, `version`).
- `input`/`output` reference [`bioschemas.formal-parameter`](bblocks://ogc.researchobject.ro-crate.bioschemas.formal-parameter)
  instead of a local, duplicated definition.
- All other nested shapes (`grant`, `person`, `organization`, `softwareApplication`,
  `propertyValue`, `categoryCode`, `creativeWork`, `product`, `definedTerm`, `computerLanguage`,
  `imageObject`) are kept as local, minimal `$defs`, matching the source — these are intentionally
  narrow stand-ins for the corresponding Schema.org types, not full Schema.org modeling.
- Predicate mappings in `context.jsonld` follow the published
  [RO-Crate 1.3 context](https://w3id.org/ro/crate/1.3/context) term for term: `ComputationalWorkflow`,
  `input`, and `output` map to `https://bioschemas.org/terms/...`; every other property (including
  the Bioschemas-specific `documentation`, `funding`, `softwareRequirements` — not just the ones
  that are genuinely Schema.org terms) maps to a plain `http://schema.org/` predicate, exactly as
  RO-Crate's context does.

  **Note on a Bioschemas inconsistency:** Bioschemas' own companion
  [type-level JSON-LD](https://github.com/BioSchemas/specifications/blob/main/ComputationalWorkflow/jsonld/type/ComputationalWorkflow_v1.0-RELEASE.json)
  declares these same terms under a *different*, non-equivalent namespace —
  `https://discovery.biothings.io/view/bioschemastypes/...` — which is neither `owl:sameAs` nor
  otherwise linked to the `bioschemas.org/terms/...` IRIs RO-Crate's context uses. Since RO-Crate is
  this register's equivalence target, `bioschemas.org/terms/...` (and plain `schema:` predicates)
  win here; `bioschemastypes:` is not used. Worth flagging upstream to Bioschemas/RO-Crate rather
  than silently working around it.

## Example provenance

The example is adapted from [WorkflowHub workflow 49](https://workflowhub.eu/workflows/49), one of
the Bioschemas profile's own published examples — property names `inputs`/`outputs` in the original
are corrected to the profile's own `input`/`output`, and `dateCreated`/`dateModified` are trimmed to
plain dates to match this block's `format: date`.
