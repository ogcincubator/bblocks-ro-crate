
# Bioschemas FormalParameter (Schema)

`ogc.researchobject.ro-crate.bioschemas.formal-parameter` *v1.0.0*

An identified variable standing for an actual value consumed or produced by a computational workflow, e.g. a [ComputationalWorkflow](bblocks://ogc.researchobject.ro-crate.bioschemas.computational-workflow) input or output.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## Provenance

Converted from the Bioschemas [FormalParameter 1.0-RELEASE](https://bioschemas.org/profiles/FormalParameter/1.0-RELEASE)
profile's `$validation` block (JSON Schema draft-07), as published in
[`BioSchemas/specifications`](https://github.com/BioSchemas/specifications/tree/main/FormalParameter).

## Deviations from the source profile

- The source's non-standard `owl:cardinality` annotations and top-level `required`/`recommended`/
  `optional` triage are dropped in favor of plain JSON Schema `required`. Per the source profile,
  `name` is required; `additionalType`, `description`, and `encodingFormat` are recommended but not
  enforced here; the rest are optional.
- `encodingFormat` is typed as a URI (or array of URIs) rather than bound to the source's
  `edmoformats` vocabulary constraint (children of [EDAM](http://edamontology.org/)
  [`format_1915`](http://edamontology.org/format_1915)) — enforcing that would need a
  service-backed vocabulary validator plugin, out of scope for this conversion.
- Predicate mappings in `context.jsonld` follow the published
  [RO-Crate 1.3 context](https://w3id.org/ro/crate/1.3/context) term for term: `FormalParameter`
  maps to `https://bioschemas.org/terms/FormalParameter`; every property (including the
  Bioschemas-specific `defaultValue`/`valueRequired`/`encodingFormat`, not just the ones that are
  genuinely Schema.org terms) maps to a plain `http://schema.org/` predicate, exactly as RO-Crate's
  context does.

  **Note on a Bioschemas inconsistency:** Bioschemas' own companion
  [type-level JSON-LD](https://github.com/BioSchemas/specifications/blob/main/FormalParameter/jsonld/type/FormalParameter_v1.0-RELEASE.json)
  declares these same terms under a *different*, non-equivalent namespace —
  `https://discovery.biothings.io/view/bioschemastypes/...` — which is neither `owl:sameAs` nor
  otherwise linked to the `bioschemas.org/terms/...` IRIs RO-Crate's context uses. Since RO-Crate is
  this register's equivalence target, `bioschemas.org/terms/...` (and plain `schema:` predicates)
  win here; `bioschemastypes:` is not used. Worth flagging upstream to Bioschemas/RO-Crate rather
  than silently working around it.

## Examples

### Tabular species-count input parameter
A `FormalParameter` describing a workflow input, adapted from [WorkflowHub workflow 49](https://workflowhub.eu/workflows/49) — see [`bioschemas.computational-workflow`](bblocks://ogc.researchobject.ro-crate.bioschemas.computational-workflow) for the full workflow this belongs to.

#### json
```json
{
  "name": "0_Input",
  "encodingFormat": "http://edamontology.org/format_3752",
  "additionalType": "http://edamontology.org/data_3707",
  "description": "Species count. A tabular file with observation data. Must at least contain three columns 'observation.unit' which associate year and location (alternatively, you can have this column split in 2 columns named 'year' and 'location'), 'species.code' with species ID and 'number' for abundance."
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/bioschemas/formal-parameter/context.jsonld",
  "name": "0_Input",
  "encodingFormat": "http://edamontology.org/format_3752",
  "additionalType": "http://edamontology.org/data_3707",
  "description": "Species count. A tabular file with observation data. Must at least contain three columns 'observation.unit' which associate year and location (alternatively, you can have this column split in 2 columns named 'year' and 'location'), 'species.code' with species ID and 'number' for abundance."
}
```

#### ttl
```ttl
@prefix schema1: <http://schema.org/> .

[] schema1:additionalType "http://edamontology.org/data_3707" ;
    schema1:description "Species count. A tabular file with observation data. Must at least contain three columns 'observation.unit' which associate year and location (alternatively, you can have this column split in 2 columns named 'year' and 'location'), 'species.code' with species ID and 'number' for abundance." ;
    schema1:encodingFormat "http://edamontology.org/format_3752" ;
    schema1:name "0_Input" .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
title: Bioschemas FormalParameter
description: An identified variable used to stand for the actual value(s) consumed
  or produced by a [ComputationalWorkflow](bblocks://ogc.researchobject.ro-crate.bioschemas.computational-workflow)
  step, per the Bioschemas [FormalParameter](https://bioschemas.org/profiles/FormalParameter/1.0-RELEASE)
  profile.
type: object
required:
- name
properties:
  name:
    description: The name of the item.
    type: string
    x-jsonld-id: http://schema.org/name
  identifier:
    description: Any kind of identifier for this item (e.g. an ISBN, GTIN, or UUID),
      given as a bare string, a URI, or a full `PropertyValue`.
    anyOf:
    - $ref: '#/$defs/propertyValue'
    - type: array
      items:
        $ref: '#/$defs/propertyValue'
    - type: string
    - type: array
      items:
        type: string
    - type: string
      format: uri
    - type: array
      items:
        type: string
        format: uri
    x-jsonld-id: http://schema.org/identifier
  description:
    description: A description of the item.
    type: string
    x-jsonld-id: http://schema.org/description
  additionalType:
    description: "A more specific type for the item, typically from an external vocabulary
      \u2014 commonly a term from the [EDAM](http://edamontology.org/) `data` branch
      for a FormalParameter's data type."
    oneOf:
    - type: string
      format: uri
    - type: array
      items:
        type: string
        format: uri
    x-jsonld-id: http://schema.org/additionalType
  defaultValue:
    description: The default value for the FormalParameter. Commonly only used for
      inputs.
    oneOf:
    - $ref: '#/$defs/thing'
    - type: string
    x-jsonld-id: http://schema.org/defaultValue
  valueRequired:
    description: Whether the FormalParameter must be specified. Commonly only used
      for inputs.
    type: boolean
    x-jsonld-id: http://schema.org/valueRequired
  encodingFormat:
    description: 'URL(s) of the accepted format(s). Strongly recommended: if absent,
      nothing should be assumed about the FormalParameter''s encoding formats. Recommended
      vocabulary: the [EDAM](http://edamontology.org/) `format` branch, rooted at
      [`format_1915`](http://edamontology.org/format_1915).'
    oneOf:
    - type: string
      format: uri
    - type: array
      items:
        type: string
        format: uri
    x-jsonld-id: http://schema.org/encodingFormat
$defs:
  thing:
    description: The most generic type of item, per Schema.org's `Thing`.
    type: object
    required:
    - name
    properties:
      name:
        type: string
        x-jsonld-id: http://schema.org/name
      identifier:
        type: string
        x-jsonld-id: http://schema.org/identifier
      url:
        type: string
        format: uri
        x-jsonld-id: http://schema.org/url
      additionalType:
        type: string
        format: uri
        x-jsonld-id: http://schema.org/additionalType
  propertyValue:
    description: A property-value pair, per Schema.org's `PropertyValue`.
    type: object
    properties:
      name:
        type: string
        x-jsonld-id: http://schema.org/name
      identifier:
        type: string
        x-jsonld-id: http://schema.org/identifier
      url:
        type: string
        format: uri
        x-jsonld-id: http://schema.org/url
      additionalType:
        type: string
        format: uri
        x-jsonld-id: http://schema.org/additionalType
      propertyID:
        type: string
        x-jsonld-id: http://schema.org/propertyID
x-jsonld-extra-terms:
  FormalParameter: https://bioschemas.org/terms/FormalParameter
x-jsonld-prefixes:
  bioschemas: https://bioschemas.org/terms/
  schema: http://schema.org/

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/bioschemas/formal-parameter/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/bioschemas/formal-parameter/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "FormalParameter": "bioschemas:FormalParameter",
    "name": "schema:name",
    "identifier": {
      "@context": {
        "url": "schema:url",
        "propertyID": "schema:propertyID"
      },
      "@id": "schema:identifier"
    },
    "description": "schema:description",
    "additionalType": "schema:additionalType",
    "defaultValue": {
      "@context": {
        "url": "schema:url"
      },
      "@id": "schema:defaultValue"
    },
    "valueRequired": "schema:valueRequired",
    "encodingFormat": "schema:encodingFormat",
    "bioschemas": "https://bioschemas.org/terms/",
    "schema": "http://schema.org/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/bioschemas/formal-parameter/context.jsonld)

## Sources

* [Bioschemas FormalParameter profile 1.0-RELEASE](https://bioschemas.org/profiles/FormalParameter/1.0-RELEASE)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-ro-crate](https://github.com/ogcincubator/bblocks-ro-crate)
* Path: `_sources/bioschemas/formal-parameter`

