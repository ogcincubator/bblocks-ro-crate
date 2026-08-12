This block reconstructs the [RO-Crate 1.3 JSON-LD context](https://w3id.org/ro/crate/1.3/context)
from smaller, independently reusable vocabulary building blocks, rather than copying the context as
one large opaque file. The original context is a flat list of 3069 term mappings; splitting it by
vocabulary source (the split RO-Crate's own
[metadata specification](https://www.researchobject.org/ro-crate/specification/1.3/metadata.html#additional-metadata-standards)
already documents in prose) makes each vocabulary's provenance explicit and lets other blocks import
just the vocabulary fragment they need instead of the whole thing.

## Composition

| Source | Building block | Terms |
|---|---|---|
| Schema.org | [`ro-crate.vocab.schema-org`](bblocks://ogc.researchobject.ro-crate.vocab.schema-org) | 3005 |
| PCDM | [`ro-crate.vocab.pcdm`](bblocks://ogc.researchobject.ro-crate.vocab.pcdm) | 5 |
| PROF | [`ro-crate.vocab.prof`](bblocks://ogc.researchobject.ro-crate.vocab.prof) | 8 |
| Dublin Core Terms | [`ro-crate.vocab.dcterms`](bblocks://ogc.researchobject.ro-crate.vocab.dcterms) | 2 |
| IANA link relations | [`ro-crate.vocab.iana-relations`](bblocks://ogc.researchobject.ro-crate.vocab.iana-relations) | 1 |
| Bioschemas | [`ro-crate.vocab.bioschemas`](bblocks://ogc.researchobject.ro-crate.vocab.bioschemas) | 4 |
| GeoSPARQL | [`ro-crate.vocab.geosparql`](bblocks://ogc.researchobject.ro-crate.vocab.geosparql) | 2 |
| CodeMeta | [`ro-crate.vocab.codemeta`](bblocks://ogc.researchobject.ro-crate.vocab.codemeta) | 10 |
| PROV / PAV | [`ro-crate.vocab.prov-pav`](bblocks://ogc.researchobject.ro-crate.vocab.prov-pav) | 7 |
| ro-terms | [`ro-crate.vocab.ro-terms`](bblocks://ogc.researchobject.ro-crate.vocab.ro-terms) | 1 |
| *(this block)* RO-Crate-specific overrides | `File`, `Journal`, `HTML` | 3 |
| *(this block)* Namespace prefix declarations | `pcdm`, `bibo`, `cc`, `dct`, `foaf`, `prof`, `profrole`, `rdf`, `rdfa`, `rdfs`, `frapo`, `rel`, `pav`, `prov`, `wfdesc`, `wfprov`, `roterms`, `relation`, `wf4ever`, `vann`, `geosparql` | 21 |

3005 + 5 + 8 + 2 + 1 + 4 + 2 + 10 + 7 + 1 + 3 + 21 = **3069**, matching the original context exactly.

## Why the schema is a no-op

The postprocessor assembles a block's JSON-LD context from its own `context.jsonld` plus the
contexts of every block reachable through `bblocks://` references in its JSON Schema — context
assembly is driven by schema `$ref` resolution, not a standalone mechanism. None of these blocks
constrain any real data shape (they are pure vocabulary/term-mapping fragments), so each carries an
unconstrained `type: object` schema whose only purpose is to be a valid `$ref` target. Applications
should use the **assembled context** (`build/.../context.jsonld` for this block), not the source
files, when processing RO-Crate JSON-LD.

## Notes on provenance

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
