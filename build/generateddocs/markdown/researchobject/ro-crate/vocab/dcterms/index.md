
# Dublin Core Terms vocabulary (Model)

`ogc.researchobject.ro-crate.vocab.dcterms` *v1.0.0*

Dublin Core Terms used by RO-Crate (`conformsTo`, `Standard`).

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
title: Dublin Core Terms vocabulary
description: 'Unconstrained carrier schema: this block''s content is its JSON-LD context,
  not a data shape. The schema exists only so other blocks can `$ref` it via `bblocks://`
  and inherit the context.'
type: object
x-jsonld-extra-terms:
  conformsTo: http://purl.org/dc/terms/conformsTo
  Standard: http://purl.org/dc/terms/Standard

```

Links to the schema:

* YAML version: [schema.yaml](https://raw.githubusercontent.com/ogcincubator/bblocks-ro-crate/undefined/build/annotated/researchobject/ro-crate/vocab/dcterms/schema.json)
* JSON version: [schema.json](https://raw.githubusercontent.com/ogcincubator/bblocks-ro-crate/undefined/build/annotated/researchobject/ro-crate/vocab/dcterms/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "conformsTo": "http://purl.org/dc/terms/conformsTo",
    "Standard": "http://purl.org/dc/terms/Standard",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://raw.githubusercontent.com/ogcincubator/bblocks-ro-crate/undefined/build/annotated/researchobject/ro-crate/vocab/dcterms/context.jsonld)

## Sources

* [DCMI Metadata Terms](http://purl.org/dc/terms/)
* [RO-Crate 1.3 JSON-LD Context](https://w3id.org/ro/crate/1.3/context)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-ro-crate](https://github.com/ogcincubator/bblocks-ro-crate)
* Path: `_sources/vocab/dcterms`

