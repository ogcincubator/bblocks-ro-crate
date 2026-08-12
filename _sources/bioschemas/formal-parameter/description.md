## Provenance

Converted from the Bioschemas [FormalParameter 1.0-RELEASE](https://bioschemas.org/profiles/FormalParameter/1.0-RELEASE)
profile's `$validation` block (JSON Schema draft-07), as published in
[`BioSchemas/specifications`](https://github.com/BioSchemas/specifications/tree/main/FormalParameter).

## Deviations from the source profile

- The source's non-standard `owl:cardinality` annotations and top-level `required`/`recommended`/
  `optional` triage are dropped in favor of plain JSON Schema `required`. Per the source profile,
  `name` is required; `additionalType`, `description`, and `encodingFormat` are recommended but not
  enforced here; the rest are optional.
- `encodingFormat` is typed as a URI (or array of URIs) rather than bound to the source's
  `edmoformats` vocabulary constraint (children of [EDAM](http://edamontology.org/)
  [`format_1915`](http://edamontology.org/format_1915)) — enforcing that would need a
  service-backed vocabulary validator plugin, out of scope for this conversion.
- Predicate mappings in `context.jsonld` follow the published
  [RO-Crate 1.3 context](https://w3id.org/ro/crate/1.3/context) term for term: `FormalParameter`
  maps to `https://bioschemas.org/terms/FormalParameter`; every property (including the
  Bioschemas-specific `defaultValue`/`valueRequired`/`encodingFormat`, not just the ones that are
  genuinely Schema.org terms) maps to a plain `http://schema.org/` predicate, exactly as RO-Crate's
  context does.

  **Note on a Bioschemas inconsistency:** Bioschemas' own companion
  [type-level JSON-LD](https://github.com/BioSchemas/specifications/blob/main/FormalParameter/jsonld/type/FormalParameter_v1.0-RELEASE.json)
  declares these same terms under a *different*, non-equivalent namespace —
  `https://discovery.biothings.io/view/bioschemastypes/...` — which is neither `owl:sameAs` nor
  otherwise linked to the `bioschemas.org/terms/...` IRIs RO-Crate's context uses. Since RO-Crate is
  this register's equivalence target, `bioschemas.org/terms/...` (and plain `schema:` predicates)
  win here; `bioschemastypes:` is not used. Worth flagging upstream to Bioschemas/RO-Crate rather
  than silently working around it.
