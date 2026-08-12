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
per source vocabulary. Most of these vocabularies aren't RO-Crate-specific, so — per the
[cross-domain model](https://github.com/ogcincubator/cross-domain-model) register's inclusion
policy (international/industry standards only) — they're imported from there (or from the
[PROV schema](https://github.com/ogcincubator/bblock-prov-schema) register) rather than duplicated
locally:

- `cross-domain.schema-org` — the Schema.org vocabulary (3005 terms)
- `cross-domain.pcdm` — Portland Common Data Model
- `cross-domain.prof` — W3C Profiles Vocabulary
- `cross-domain.dcterms` — Dublin Core Terms
- `cross-domain.iana-relations` — IANA link relations
- `cross-domain.geosparql` — GeoSPARQL
- `cross-domain.codemeta` — CodeMeta 3.0
- `cross-domain.pav` — PAV (Provenance, Authoring and Versioning)
- `ogc-utils.prov` — PROV-O (from the PROV schema register)
- `bioschemas/computational-workflow`, `bioschemas/formal-parameter` — real structural schemas for
  Bioschemas' ComputationalWorkflow / FormalParameter profiles (local: not yet a standard, kept out
  of the cross-domain register per policy)
- `vocab/ro-terms` — the RO-Crate community namespace (local: RO-Crate's own, not a shared standard)

...and a `context` block that assembles all of them plus RO-Crate's own overrides (`File`,
`Journal`, `HTML`) and namespace prefixes, reproducing the original context term for term. See
[`_sources/context/description.md`](_sources/context/description.md) for the full composition table
and provenance notes.

Most of the imported vocabulary blocks are vocabulary-only — a JSON-LD `context.jsonld`, with no
meaningful JSON Schema of its own (the schema is an unconstrained placeholder, present only so the
postprocessor's `$ref`-driven context assembly can pick it up). Two exceptions carry real structural
schemas, pulled in here only for their context mapping (their own validation isn't exercised by the
`context` block): `ogc-utils.prov` (Agents/Activities/Entities mixin) and the two `bioschemas`
blocks (ComputationalWorkflow/FormalParameter, converted from Bioschemas' own `$validation` JSON
Schema — see their `description.md` for the conversion notes). RO-Crate's other structural rules for
entities (Root Data Entity, Data Entities, Contextual Entities, etc.) are not modeled here yet — this
register otherwise covers vocabulary reconstruction only.

## Building and viewing locally

See [USAGE.md](USAGE.md) and the
[OGC Building Blocks authoring documentation](https://ogcincubator.github.io/bblocks-docs/) for how
to run the postprocessor (`build.sh`) and viewer (`view.sh`) locally.

## How this register was built, and how it was checked

The blocks above were derived by parsing RO-Crate's original `context.jsonld` and partitioning
its 3069 term mappings by source vocabulary, matching the grouping already described in prose in the
[metadata specification](https://www.researchobject.org/ro-crate/specification/1.3/metadata.html#additional-metadata-standards):
the bulk (3005 terms) is a straight Schema.org pass-through, and the rest splits cleanly into PCDM,
PROF, Dublin Core Terms, IANA link relations, Bioschemas, GeoSPARQL, CodeMeta, PROV, PAV, and the
RO-Crate community namespace, plus a few RO-Crate-specific overrides and 25 bare namespace prefix
declarations.

Each vocabulary fragment became its own building block: just a `context.jsonld`, no meaningful JSON
Schema. Context assembly in the bblocks postprocessor is driven by schema `$ref` resolution (a block
inherits another's JSON-LD context by referencing its schema via `bblocks://`), not by a standalone
context-merge mechanism — so each of these blocks carries an unconstrained `type: object` schema
whose only purpose is to be a valid `$ref` target (the one exception is `ogc.ogc-utils.prov`, a real
structural PROV schema imported from the `prov-schema` register). The `context` block then aggregates
all of them via `allOf`/`$ref` and adds RO-Crate's own overrides and prefixes on top.

This was verified by actually running the postprocessor (`ghcr.io/opengeospatial/bblocks-postprocess`
via Docker, full clean run, all pipeline steps) — 0 errors — and then diffing the assembled output
context (`build-local/annotated/researchobject/ro-crate/context/context.jsonld`) against the original
`https://w3id.org/ro/crate/1.3/context` term by term. The postprocessor compacts many absolute
`http://schema.org/...` URIs into prefixed forms (e.g. `schema:Dataset`); resolving those compact
IRIs back through their prefix definitions confirmed all 3069 original terms are present and expand
to their original absolute URI.

Most of the vocabulary blocks now come from the [cross-domain
model](https://github.com/ogcincubator/cross-domain-model) and [PROV
schema](https://github.com/ogcincubator/bblock-prov-schema) registers rather than being duplicated
locally (see [`_sources/context/description.md`](_sources/context/description.md#why-schemaorg-must-be-last-in-allof)
for why). The real, structural PROV schema brings in the full PROV-O vocabulary rather than just
`wasDerivedFrom`, so the assembled context now has 3188 terms — 119 more than the original — but
every original term is still present at its original IRI, and `schema-org` is deliberately placed
last in the `allOf` list so its bindings win the handful of term-name collisions with PROV-O
(`Person`, `Organization`, `name`, `value`, etc.). Two terms (`agent`, `wasDerivedFrom`) gained an
explicit `@type: @id` they lacked in the original spec context — a fix, not a regression.

Not yet done: examples/tests per block, and modeling RO-Crate's structural entities (Root Data
Entity, Data Entities, Contextual Entities, etc.) as JSON Schema blocks — this register currently
covers vocabulary reconstruction only.
