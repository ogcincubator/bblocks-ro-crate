
# PCDM vocabulary (Model)

`ogc.researchobject.ro-crate.vocab.pcdm` *v1.0.0*

Portland Common Data Model terms used by RO-Crate to describe repositories and collections of digital objects (`RepositoryObject`, `RepositoryCollection`, `RepositoryFile`, `hasMember`, `hasFile`).

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
title: PCDM vocabulary
description: 'Unconstrained carrier schema: this block''s content is its JSON-LD context,
  not a data shape. The schema exists only so other blocks can `$ref` it via `bblocks://`
  and inherit the context.'
type: object
x-jsonld-extra-terms:
  hasFile: http://pcdm.org/models#hasFile
  hasMember: http://pcdm.org/models#hasMember
  RepositoryCollection: http://pcdm.org/models#Collection
  RepositoryObject: http://pcdm.org/models#Object
  RepositoryFile: http://pcdm.org/models#File

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/vocab/pcdm/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/vocab/pcdm/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "hasFile": "http://pcdm.org/models#hasFile",
    "hasMember": "http://pcdm.org/models#hasMember",
    "RepositoryCollection": "http://pcdm.org/models#Collection",
    "RepositoryObject": "http://pcdm.org/models#Object",
    "RepositoryFile": "http://pcdm.org/models#File",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/vocab/pcdm/context.jsonld)

## Sources

* [Portland Common Data Model (PCDM)](https://pcdm.org/2016/04/18/models)
* [RO-Crate 1.3 JSON-LD Context](https://w3id.org/ro/crate/1.3/context)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-ro-crate](https://github.com/ogcincubator/bblocks-ro-crate)
* Path: `_sources/vocab/pcdm`

