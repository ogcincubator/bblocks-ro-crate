
# GeoSPARQL vocabulary (Model)

`ogc.researchobject.ro-crate.vocab.geosparql` *v1.0.0*

GeoSPARQL terms used by RO-Crate to support geometry on [Place](https://www.researchobject.org/ro-crate/specification/1.3/contextual-entities.html#places) contextual entities (`Geometry`, `asWKT`).

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
title: GeoSPARQL vocabulary
description: 'Unconstrained carrier schema: this block''s content is its JSON-LD context,
  not a data shape. The schema exists only so other blocks can `$ref` it via `bblocks://`
  and inherit the context.'
type: object
x-jsonld-extra-terms:
  Geometry: http://www.opengis.net/ont/geosparql#Geometry
  asWKT: http://www.opengis.net/ont/geosparql#asWKT

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/vocab/geosparql/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/vocab/geosparql/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "Geometry": "http://www.opengis.net/ont/geosparql#Geometry",
    "asWKT": "http://www.opengis.net/ont/geosparql#asWKT",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/vocab/geosparql/context.jsonld)

## Sources

* [OGC GeoSPARQL](http://www.opengis.net/ont/geosparql)
* [RO-Crate 1.3 JSON-LD Context](https://w3id.org/ro/crate/1.3/context)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-ro-crate](https://github.com/ogcincubator/bblocks-ro-crate)
* Path: `_sources/vocab/geosparql`

