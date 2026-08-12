
# IANA link relations vocabulary (Model)

`ogc.researchobject.ro-crate.vocab.iana-relations` *v1.0.0*

The IANA link relation used by RO-Crate to mark preferred citation targets (`cite-as`, [RFC 8574](https://www.rfc-editor.org/rfc/rfc8574)).

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
title: IANA link relations vocabulary
description: 'Unconstrained carrier schema: this block''s content is its JSON-LD context,
  not a data shape. The schema exists only so other blocks can `$ref` it via `bblocks://`
  and inherit the context.'
type: object
x-jsonld-extra-terms:
  cite-as: http://www.iana.org/assignments/relation/cite-as

```

Links to the schema:

* YAML version: [schema.yaml](https://raw.githubusercontent.com/ogcincubator/bblocks-ro-crate/undefined/build/annotated/researchobject/ro-crate/vocab/iana-relations/schema.json)
* JSON version: [schema.json](https://raw.githubusercontent.com/ogcincubator/bblocks-ro-crate/undefined/build/annotated/researchobject/ro-crate/vocab/iana-relations/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "cite-as": "http://www.iana.org/assignments/relation/cite-as",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://raw.githubusercontent.com/ogcincubator/bblocks-ro-crate/undefined/build/annotated/researchobject/ro-crate/vocab/iana-relations/context.jsonld)

## Sources

* [IANA Link Relations registry](http://www.iana.org/assignments/relation/)
* [RO-Crate 1.3 JSON-LD Context](https://w3id.org/ro/crate/1.3/context)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-ro-crate](https://github.com/ogcincubator/bblocks-ro-crate)
* Path: `_sources/vocab/iana-relations`

