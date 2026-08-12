
# RO-Crate terms vocabulary (Model)

`ogc.researchobject.ro-crate.vocab.ro-terms` *v1.0.0*

The custom RO-Crate community namespace, used in the core context for `localPath`.

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
title: RO-Crate terms vocabulary
description: 'Unconstrained carrier schema: this block''s content is its JSON-LD context,
  not a data shape. The schema exists only so other blocks can `$ref` it via `bblocks://`
  and inherit the context.'
type: object
x-jsonld-extra-terms:
  localPath: https://w3id.org/ro/terms#localPath

```

Links to the schema:

* YAML version: [schema.yaml](https://raw.githubusercontent.com/ogcincubator/bblocks-ro-crate/undefined/build/annotated/researchobject/ro-crate/vocab/ro-terms/schema.json)
* JSON version: [schema.json](https://raw.githubusercontent.com/ogcincubator/bblocks-ro-crate/undefined/build/annotated/researchobject/ro-crate/vocab/ro-terms/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "localPath": "https://w3id.org/ro/terms#localPath",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://raw.githubusercontent.com/ogcincubator/bblocks-ro-crate/undefined/build/annotated/researchobject/ro-crate/vocab/ro-terms/context.jsonld)

## Sources

* [ro-terms](https://github.com/ResearchObject/ro-terms)
* [RO-Crate 1.3 JSON-LD Context](https://w3id.org/ro/crate/1.3/context)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-ro-crate](https://github.com/ogcincubator/bblocks-ro-crate)
* Path: `_sources/vocab/ro-terms`

