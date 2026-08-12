
# PROV / PAV vocabulary (Model)

`ogc.researchobject.ro-crate.vocab.prov-pav` *v1.0.0*

W3C PROV-O and PAV (Provenance, Authoring and Versioning) terms used by RO-Crate for provenance (`wasDerivedFrom`, `importedFrom`, `importedOn`, `importedBy`, `retrievedFrom`, `retrievedOn`, `retrievedBy`).

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
title: PROV / PAV vocabulary
description: 'Unconstrained carrier schema: this block''s content is its JSON-LD context,
  not a data shape. The schema exists only so other blocks can `$ref` it via `bblocks://`
  and inherit the context.'
type: object
x-jsonld-extra-terms:
  wasDerivedFrom: http://www.w3.org/ns/prov#wasDerivedFrom
  importedFrom: http://purl.org/pav/importedFrom
  importedOn: http://purl.org/pav/importedOn
  importedBy: http://purl.org/pav/importedBy
  retrievedFrom: http://purl.org/pav/retrievedFrom
  retrievedOn: http://purl.org/pav/retrievedOn
  retrievedBy: http://purl.org/pav/retrievedBy

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/vocab/prov-pav/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/vocab/prov-pav/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "wasDerivedFrom": "http://www.w3.org/ns/prov#wasDerivedFrom",
    "importedFrom": "http://purl.org/pav/importedFrom",
    "importedOn": "http://purl.org/pav/importedOn",
    "importedBy": "http://purl.org/pav/importedBy",
    "retrievedFrom": "http://purl.org/pav/retrievedFrom",
    "retrievedOn": "http://purl.org/pav/retrievedOn",
    "retrievedBy": "http://purl.org/pav/retrievedBy",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/vocab/prov-pav/context.jsonld)

## Sources

* [PROV-O: The PROV Ontology](https://www.w3.org/ns/prov#)
* [Provenance, Authoring and Versioning (PAV) ontology](http://purl.org/pav/)
* [RO-Crate 1.3 JSON-LD Context](https://w3id.org/ro/crate/1.3/context)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-ro-crate](https://github.com/ogcincubator/bblocks-ro-crate)
* Path: `_sources/vocab/prov-pav`

