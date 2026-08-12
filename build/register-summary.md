# RO-Crate Building Blocks

Building blocks reconstructing the [RO-Crate 1.3](https://www.researchobject.org/ro-crate/specification/1.3/)
JSON-LD context from independently reusable vocabulary fragments.


This register splits the [RO-Crate 1.3 JSON-LD context](https://w3id.org/ro/crate/1.3/context) into
one building block per source vocabulary (Schema.org, PCDM, PROF, Dublin Core Terms, IANA link
relations, Bioschemas, GeoSPARQL, CodeMeta, PROV/PAV, ro-terms), plus a block that assembles them
back together with RO-Crate's own term overrides and namespace prefixes. The assembled context is
equivalent, term for term, to the original. See the
[`ro-crate.context`](bblocks://ogc.researchobject.ro-crate.context) block for the full composition and
provenance notes.


## Building Blocks

### `ogc.researchobject.ro-crate.vocab.prof` — PROF vocabulary

**Type:** model

W3C Profiles Vocabulary (PROF) terms used by RO-Crate to describe [profiles](https://www.researchobject.org/ro-crate/specification/1.3/profiles.html).

### `ogc.researchobject.ro-crate.vocab.bioschemas` — Bioschemas vocabulary

**Type:** model

Terms proposed by the Bioschemas ComputationalWorkflow and FormalParameter profiles for inclusion in Schema.org, used by RO-Crate to describe [workflows](https://www.researchobject.org/ro-crate/specification/1.3/workflows.html).

### `ogc.researchobject.ro-crate.vocab.pcdm` — PCDM vocabulary

**Type:** model

Portland Common Data Model terms used by RO-Crate to describe repositories and collections of digital objects (`RepositoryObject`, `RepositoryCollection`, `RepositoryFile`, `hasMember`, `hasFile`).

### `ogc.researchobject.ro-crate.vocab.codemeta` — CodeMeta vocabulary

**Type:** model

CodeMeta 3.0 terms used by RO-Crate to describe software (`buildInstructions`, `developmentStatus`, `continuousIntegration`, `embargoEndDate`, `hasSourceCode`, `isSourceCodeOf`, `issueTracker`, `readme`, `referencePublication`, `softwareSuggestions`).

### `ogc.researchobject.ro-crate.vocab.geosparql` — GeoSPARQL vocabulary

**Type:** model

GeoSPARQL terms used by RO-Crate to support geometry on [Place](https://www.researchobject.org/ro-crate/specification/1.3/contextual-entities.html#places) contextual entities (`Geometry`, `asWKT`).

### `ogc.researchobject.ro-crate.vocab.schema-org` — Schema.org vocabulary

**Type:** model

The full [Schema.org](https://schema.org/) term vocabulary, as pinned by the RO-Crate 1.3 JSON-LD context: every Schema.org type and property name mapped 1:1 to its `http://schema.org/` URI.

### `ogc.researchobject.ro-crate.vocab.ro-terms` — RO-Crate terms vocabulary

**Type:** model

The custom RO-Crate community namespace, used in the core context for `localPath`.

### `ogc.researchobject.ro-crate.vocab.dcterms` — Dublin Core Terms vocabulary

**Type:** model

Dublin Core Terms used by RO-Crate (`conformsTo`, `Standard`).

### `ogc.researchobject.ro-crate.vocab.prov-pav` — PROV / PAV vocabulary

**Type:** model

W3C PROV-O and PAV (Provenance, Authoring and Versioning) terms used by RO-Crate for provenance (`wasDerivedFrom`, `importedFrom`, `importedOn`, `importedBy`, `retrievedFrom`, `retrievedOn`, `retrievedBy`).

### `ogc.researchobject.ro-crate.vocab.iana-relations` — IANA link relations vocabulary

**Type:** model

The IANA link relation used by RO-Crate to mark preferred citation targets (`cite-as`, [RFC 8574](https://www.rfc-editor.org/rfc/rfc8574)).

### `ogc.researchobject.ro-crate.context` — RO-Crate JSON-LD Context

**Type:** model

Assembles the RO-Crate 1.3 JSON-LD context from its constituent vocabulary building blocks, and adds the RO-Crate-specific term overrides (`File`, `Journal`, `HTML`) and namespace prefix declarations. The context produced by this block is equivalent, term for term, to <https://w3id.org/ro/crate/1.3/context>.

