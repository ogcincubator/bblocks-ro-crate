# RO-Crate Building Blocks

[OGC Building Blocks](https://blocks.ogc.org) reconstructing the
[RO-Crate 1.3](https://www.researchobject.org/ro-crate/specification/1.3/) JSON-LD context from
independently reusable vocabulary fragments.

## What's here

The RO-Crate 1.3 [JSON-LD context](https://w3id.org/ro/crate/1.3/context) is a flat list of 3069
term mappings: the bulk of it is a straight pass-through of the [Schema.org](https://schema.org/)
vocabulary, plus a handful of terms pulled in from nine other vocabularies (documented in prose in
RO-Crate's own [metadata specification](https://www.researchobject.org/ro-crate/specification/1.3/metadata.html#additional-metadata-standards)),
plus a few RO-Crate-specific term overrides and namespace prefix declarations.

This register splits that context along those same vocabulary boundaries into one building block
per source vocabulary:

- `vocab/schema-org` — the Schema.org vocabulary (3005 terms)
- `vocab/pcdm` — Portland Common Data Model
- `vocab/prof` — W3C Profiles Vocabulary
- `vocab/dcterms` — Dublin Core Terms
- `vocab/iana-relations` — IANA link relations
- `vocab/bioschemas` — Bioschemas ComputationalWorkflow / FormalParameter
- `vocab/geosparql` — GeoSPARQL
- `vocab/codemeta` — CodeMeta 3.0
- `vocab/prov-pav` — PROV-O / PAV
- `vocab/ro-terms` — the RO-Crate community namespace

...and a `context` block that assembles all of them plus RO-Crate's own overrides (`File`,
`Journal`, `HTML`) and namespace prefixes, reproducing the original context term for term. See
[`_sources/context/description.md`](_sources/context/description.md) for the full composition table
and provenance notes.

Each of these blocks is vocabulary-only — a JSON-LD `context.jsonld`, with no meaningful JSON Schema
of its own (the schema is an unconstrained placeholder, present only so the postprocessor's
`$ref`-driven context assembly can pick it up). RO-Crate's structural rules for entities (Root Data
Entity, Data Entities, Contextual Entities, etc.) are not modeled here yet — this register currently
covers vocabulary reconstruction only.

## Building and viewing locally

See [USAGE.md](USAGE.md) and the
[OGC Building Blocks authoring documentation](https://ogcincubator.github.io/bblocks-docs/) for how
to run the postprocessor (`build.sh`) and viewer (`view.sh`) locally.

## How this register was built, and how it was checked

The 11 blocks above were derived by parsing RO-Crate's original `context.jsonld` and partitioning
its 3069 term mappings by source vocabulary, matching the grouping already described in prose in the
[metadata specification](https://www.researchobject.org/ro-crate/specification/1.3/metadata.html#additional-metadata-standards):
the bulk (3005 terms) is a straight Schema.org pass-through, and the rest splits cleanly into PCDM,
PROF, Dublin Core Terms, IANA link relations, Bioschemas, GeoSPARQL, CodeMeta, PROV/PAV, and the
RO-Crate community namespace, plus a few RO-Crate-specific overrides and 25 bare namespace prefix
declarations.

Each vocabulary fragment became its own building block: just a `context.jsonld`, no meaningful JSON
Schema. Context assembly in the bblocks postprocessor is driven by schema `$ref` resolution (a block
inherits another's JSON-LD context by referencing its schema via `bblocks://`), not by a standalone
context-merge mechanism — so each of these blocks carries an unconstrained `type: object` schema
whose only purpose is to be a valid `$ref` target. The `context` block then aggregates all ten via
`allOf`/`$ref` and adds RO-Crate's own overrides and prefixes on top.

This was verified by actually running the postprocessor (`ghcr.io/opengeospatial/bblocks-postprocess`
via Docker, full clean run, all six pipeline steps) — 11/11 blocks processed with 0 errors — and then
diffing the assembled output context
(`build-local/annotated/researchobject/ro-crate/context/context.jsonld`) against the original
`https://w3id.org/ro/crate/1.3/context` term by term. The postprocessor compacts many absolute
`http://schema.org/...` URIs into prefixed forms (e.g. `schema:Dataset`); resolving those compact
IRIs back through their prefix definitions confirmed all 3069 original terms are present and expand
to their original absolute URI, with zero genuine mismatches — the only addition is `@version: 1.1`,
a JSON-LD processing directive, not a term.

Not yet done: examples/tests per block, and modeling RO-Crate's structural entities (Root Data
Entity, Data Entities, Contextual Entities, etc.) as JSON Schema blocks — this register currently
covers vocabulary reconstruction only.
