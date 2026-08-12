# RO-Crate Building Blocks

Building blocks reconstructing the [RO-Crate 1.3](https://www.researchobject.org/ro-crate/specification/1.3/)
JSON-LD context from independently reusable vocabulary fragments.


This register splits the [RO-Crate 1.3 JSON-LD context](https://w3id.org/ro/crate/1.3/context) into
one building block per source vocabulary (Bioschemas, ro-terms locally; Schema.org, PCDM, PROF,
Dublin Core Terms, IANA link relations, GeoSPARQL, CodeMeta, PROV, PAV imported from the
[cross-domain model](https://ogcincubator.github.io/cross-domain-model/) register and the
[PROV schema](https://ogcincubator.github.io/bblock-prov-schema/) register), plus a block that
assembles them back together with RO-Crate's own term overrides and namespace prefixes. The
assembled context is equivalent, term for term, to the original. See the
[`ro-crate.context`](bblocks://ogc.researchobject.ro-crate.context) block for the full composition and
provenance notes.


## Building Blocks

### `ogc.researchobject.ro-crate.bioschemas.formal-parameter` — Bioschemas FormalParameter

**Type:** schema

An identified variable standing for an actual value consumed or produced by a computational workflow, e.g. a [ComputationalWorkflow](bblocks://ogc.researchobject.ro-crate.bioschemas.computational-workflow) input or output.

### `ogc.researchobject.ro-crate.vocab.ro-terms` — RO-Crate terms vocabulary

**Type:** model

The custom RO-Crate community namespace, used in the core context for `localPath`.

### `ogc.researchobject.ro-crate.bioschemas.computational-workflow` — Bioschemas ComputationalWorkflow

**Type:** schema

A computational workflow — an orchestrated, repeatable pattern of activity executed by a computational process — as described by RO-Crate's [Workflow RO-Crate profile](https://www.researchobject.org/ro-crate/specification/1.3/workflows.html).

### `ogc.researchobject.ro-crate.context` — RO-Crate JSON-LD Context

**Type:** model

Assembles the RO-Crate 1.3 JSON-LD context from its constituent vocabulary building blocks, and adds the RO-Crate-specific term overrides (`File`, `Journal`, `HTML`) and namespace prefix declarations. The context produced by this block is equivalent, term for term, to <https://w3id.org/ro/crate/1.3/context>.

