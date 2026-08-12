
# Bioschemas vocabulary (Model)

`ogc.researchobject.ro-crate.vocab.bioschemas` *v1.0.0*

Terms proposed by the Bioschemas ComputationalWorkflow and FormalParameter profiles for inclusion in Schema.org, used by RO-Crate to describe [workflows](https://www.researchobject.org/ro-crate/specification/1.3/workflows.html).

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
title: Bioschemas vocabulary
description: 'Unconstrained carrier schema: this block''s content is its JSON-LD context,
  not a data shape. The schema exists only so other blocks can `$ref` it via `bblocks://`
  and inherit the context.'
type: object
x-jsonld-extra-terms:
  ComputationalWorkflow: https://bioschemas.org/terms/ComputationalWorkflow
  input: https://bioschemas.org/terms/input
  output: https://bioschemas.org/terms/output
  FormalParameter: https://bioschemas.org/terms/FormalParameter

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/vocab/bioschemas/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/vocab/bioschemas/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "ComputationalWorkflow": "https://bioschemas.org/terms/ComputationalWorkflow",
    "input": "https://bioschemas.org/terms/input",
    "output": "https://bioschemas.org/terms/output",
    "FormalParameter": "https://bioschemas.org/terms/FormalParameter",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/vocab/bioschemas/context.jsonld)

## Sources

* [Bioschemas ComputationalWorkflow profile 1.0-RELEASE](https://bioschemas.org/profiles/ComputationalWorkflow/1.0-RELEASE)
* [Bioschemas FormalParameter profile 1.0-RELEASE](https://bioschemas.org/profiles/FormalParameter/1.0-RELEASE)
* [RO-Crate 1.3 JSON-LD Context](https://w3id.org/ro/crate/1.3/context)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-ro-crate](https://github.com/ogcincubator/bblocks-ro-crate)
* Path: `_sources/vocab/bioschemas`

