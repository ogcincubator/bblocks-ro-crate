This block reconstructs the [RO-Crate 1.3 JSON-LD context](https://w3id.org/ro/crate/1.3/context)
from smaller, independently reusable vocabulary building blocks, rather than copying the context as
one large opaque file. The original context is a flat list of 3069 term mappings; splitting it by
vocabulary source (the split RO-Crate's own
[metadata specification](https://www.researchobject.org/ro-crate/specification/1.3/metadata.html#additional-metadata-standards)
already documents in prose) makes each vocabulary's provenance explicit and lets other blocks import
just the vocabulary fragment they need instead of the whole thing.

## Composition

Most of these vocabulary blocks are not RO-Crate-specific, so — per the
[cross-domain model](https://github.com/ogcincubator/cross-domain-model) register's inclusion
policy (international/industry standards only) — they live there or in the
[PROV schema](https://github.com/ogcincubator/bblock-prov-schema) register instead of being
duplicated locally. Only `bioschemas` (a proposed, not-yet-standardized vocabulary, and — unlike the
others — a pair of real structural schema blocks, not just a context passthrough) and `ro-terms`
(RO-Crate's own community namespace) remain local to this register.

| Source | Building block | Terms |
|---|---|---|
| Schema.org | [`cross-domain.schema-org`](bblocks://ogc.model.cross-domain.schema-org) | 3005 |
| PCDM | [`cross-domain.pcdm`](bblocks://ogc.model.cross-domain.pcdm) | 5 |
| PROF | [`cross-domain.prof`](bblocks://ogc.model.cross-domain.prof) | 8 |
| Dublin Core Terms | [`cross-domain.dcterms`](bblocks://ogc.model.cross-domain.dcterms) | 2 |
| IANA link relations | [`cross-domain.iana-relations`](bblocks://ogc.model.cross-domain.iana-relations) | 1 |
| Bioschemas | [`bioschemas.computational-workflow`](bblocks://ogc.researchobject.ro-crate.bioschemas.computational-workflow), [`bioschemas.formal-parameter`](bblocks://ogc.researchobject.ro-crate.bioschemas.formal-parameter) | 4 |
| GeoSPARQL | [`cross-domain.geosparql`](bblocks://ogc.model.cross-domain.geosparql) | 2 |
| CodeMeta | [`cross-domain.codemeta`](bblocks://ogc.model.cross-domain.codemeta) | 10 |
| PROV | [`ogc-utils.prov`](bblocks://ogc.ogc-utils.prov) | 1 |
| PAV | [`cross-domain.pav`](bblocks://ogc.model.cross-domain.pav) | 6 |
| ro-terms | [`ro-crate.vocab.ro-terms`](bblocks://ogc.researchobject.ro-crate.vocab.ro-terms) | 1 |
| *(this block)* RO-Crate-specific overrides | `File`, `Journal`, `HTML` | 3 |
| *(this block)* Namespace prefix declarations | `pcdm`, `bibo`, `cc`, `dct`, `foaf`, `prof`, `profrole`, `rdf`, `rdfa`, `rdfs`, `frapo`, `rel`, `pav`, `prov`, `wfdesc`, `wfprov`, `roterms`, `relation`, `wf4ever`, `vann`, `geosparql` | 21 |

3005 + 5 + 8 + 2 + 1 + 4 + 2 + 10 + 1 + 6 + 1 + 3 + 21 = **3069**, matching the original context exactly.

## Why the schema is a no-op

The postprocessor assembles a block's JSON-LD context from its own `context.jsonld` plus the
contexts of every block reachable through `bblocks://` references in its JSON Schema — context
assembly is driven by schema `$ref` resolution, not a standalone mechanism. Most of the vocabulary
blocks don't constrain any real data shape (they are pure vocabulary/term-mapping fragments), so
each carries an unconstrained `type: object` schema whose only purpose is to be a valid `$ref`
target. Two exceptions:
- `ogc.ogc-utils.prov`, a real structural PROV schema (Agents/Activities/Entities mixin) from the
  `prov-schema` register — pulled in for its `wasDerivedFrom` context mapping; its structural
  constraints have no effect here since this block is never itself validated against instance data.
- `bioschemas.computational-workflow` / `bioschemas.formal-parameter`, real structural schemas for
  RO-Crate's Workflow entities (unlike the other local vocab block, `ro-terms`, which is still a
  pure passthrough) — likewise pulled in here only for their context contributions, not validated
  as part of this block.

Applications should use the **assembled context** (`build/.../context.jsonld` for this block), not
the source files, when processing RO-Crate JSON-LD.

## Why Schema.org must be last in `allOf`

Because `ogc.ogc-utils.prov` is the *full* PROV-O vocabulary rather than a single-term passthrough,
it carries 118 terms beyond `wasDerivedFrom` (`Person`, `Organization`, `Collection`, `Role`,
`Quotation`, `InstantaneousEvent`, `name`, `value`, `agent`, ...) — several of which collide with
Schema.org term names RO-Crate actually depends on. Context assembly merges term-by-term in `allOf`
order, last write wins per term. `schema-org` is listed last specifically so its bindings win any
such collision — verified by re-checking every colliding term resolves back to `schema:*`, not
`prov:*`, after assembly. If further vocabulary blocks are added to this `allOf` in the future,
re-run the equivalence check below rather than assuming order doesn't matter.

The assembled context therefore has 3188 terms, not 3069: the 119 extra ones (118 PROV-O terms plus
`@version`) are harmless additions RO-Crate itself doesn't use, not term losses — every one of the
original 3069 terms is still present and resolves to the same IRI. Two terms gained a genuine fix
over the original spec context: `agent` and `wasDerivedFrom` are now explicitly typed `@type: @id`
(they were bare, untyped strings in the original — meaning a strict JSON-LD processor would treat
their values as string literals rather than IRI references), inherited correctly from
`ogc.ogc-utils.prov`'s definitions.

## Notes on provenance

- Bioschemas itself is inconsistent about which namespace identifies its own terms: its profile
  documents' companion type-level JSON-LD (e.g.
  [`ComputationalWorkflow_v1.0-RELEASE.json`](https://github.com/BioSchemas/specifications/blob/main/ComputationalWorkflow/jsonld/type/ComputationalWorkflow_v1.0-RELEASE.json))
  declares terms under `https://discovery.biothings.io/view/bioschemastypes/...`, while RO-Crate's
  published context uses `https://bioschemas.org/terms/...` — a different, unlinked namespace. See
  the "Deviations from the source profile" notes in
  [`bioschemas.computational-workflow`](bblocks://ogc.researchobject.ro-crate.bioschemas.computational-workflow)
  and [`bioschemas.formal-parameter`](bblocks://ogc.researchobject.ro-crate.bioschemas.formal-parameter)
  for how this was resolved (RO-Crate's namespace wins, since it's this register's equivalence
  target).
- The `wfdesc`, `wfprov`, `roterms` and `wf4ever` namespace *prefixes* are declared here (for use by
  RO-Crate profiles that want to mint compact IRIs) but none of their terms are consumed directly by
  the core RO-Crate context — so, unlike the ten vocabulary blocks above, no dependency on an actual
  `wfdesc`/`wfprov`/`ro`/`wf4ever` ontology block is required to reproduce the context term-for-term.
  The [wf4ever register](https://github.com/ogcincubator/bblocks-wf4ever) publishes blocks for these
  same vocabularies (`ogc.bbr.wf4ever.ro`, `ogc.bbr.wf4ever.wf4ever`, `ogc.bbr.wf4ever.wfprov`,
  `ogc.bbr.wf4ever.wfdesc`) which may be worth cross-linking once their declared namespace URIs are
  confirmed to match RO-Crate's (`http://purl.org/ro/...#`).
- `wasDerivedFrom` (PROV) and the `importedFrom`/`importedOn`/`importedBy`/`retrievedFrom`/
  `retrievedOn`/`retrievedBy` (PAV) terms are present in the RO-Crate context but are not itemized in
  the prose of the metadata specification — they are used by the
  [Provenance of Entities](https://www.researchobject.org/ro-crate/specification/1.3/provenance.html)
  section.
