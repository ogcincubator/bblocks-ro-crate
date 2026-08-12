
# Bioschemas ComputationalWorkflow (Schema)

`ogc.researchobject.ro-crate.bioschemas.computational-workflow` *v1.0.0*

A computational workflow — an orchestrated, repeatable pattern of activity executed by a computational process — as described by RO-Crate's [Workflow RO-Crate profile](https://www.researchobject.org/ro-crate/specification/1.3/workflows.html).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## Provenance

Converted from the Bioschemas [ComputationalWorkflow 1.0-RELEASE](https://bioschemas.org/profiles/ComputationalWorkflow/1.0-RELEASE)
profile's `$validation` block (JSON Schema draft-07), as published in
[`BioSchemas/specifications`](https://github.com/BioSchemas/specifications/tree/main/ComputationalWorkflow).
This is the profile RO-Crate's [Workflow RO-Crate](https://www.researchobject.org/ro-crate/specification/1.3/workflows.html)
specification points to for describing a crate's Main Entity.

## Deviations from the source profile

- The source's non-standard `owl:cardinality` annotations and top-level `required`/`recommended`/
  `optional` triage are dropped in favor of plain JSON Schema `required`, matching the profile's
  own `required` list (`input`, `output`, `programmingLanguage`, `name`, `url`, `creator`,
  `dateCreated`, `license`, `sdPublisher`, `version`).
- `input`/`output` reference [`bioschemas.formal-parameter`](bblocks://ogc.researchobject.ro-crate.bioschemas.formal-parameter)
  instead of a local, duplicated definition.
- All other nested shapes (`grant`, `person`, `organization`, `softwareApplication`,
  `propertyValue`, `categoryCode`, `creativeWork`, `product`, `definedTerm`, `computerLanguage`,
  `imageObject`) are kept as local, minimal `$defs`, matching the source — these are intentionally
  narrow stand-ins for the corresponding Schema.org types, not full Schema.org modeling.
- Predicate mappings in `context.jsonld` follow the published
  [RO-Crate 1.3 context](https://w3id.org/ro/crate/1.3/context) term for term: `ComputationalWorkflow`,
  `input`, and `output` map to `https://bioschemas.org/terms/...`; every other property (including
  the Bioschemas-specific `documentation`, `funding`, `softwareRequirements` — not just the ones
  that are genuinely Schema.org terms) maps to a plain `http://schema.org/` predicate, exactly as
  RO-Crate's context does.

  **Note on a Bioschemas inconsistency:** Bioschemas' own companion
  [type-level JSON-LD](https://github.com/BioSchemas/specifications/blob/main/ComputationalWorkflow/jsonld/type/ComputationalWorkflow_v1.0-RELEASE.json)
  declares these same terms under a *different*, non-equivalent namespace —
  `https://discovery.biothings.io/view/bioschemastypes/...` — which is neither `owl:sameAs` nor
  otherwise linked to the `bioschemas.org/terms/...` IRIs RO-Crate's context uses. Since RO-Crate is
  this register's equivalence target, `bioschemas.org/terms/...` (and plain `schema:` predicates)
  win here; `bioschemastypes:` is not used. Worth flagging upstream to Bioschemas/RO-Crate rather
  than silently working around it.

## Example provenance

The example is adapted from [WorkflowHub workflow 49](https://workflowhub.eu/workflows/49), one of
the Bioschemas profile's own published examples — property names `inputs`/`outputs` in the original
are corrected to the profile's own `input`/`output`, and `dateCreated`/`dateModified` are trimmed to
plain dates to match this block's `format: date`.

## Examples

### Biodiversity metrics Galaxy workflow
Adapted from [WorkflowHub workflow 49](https://workflowhub.eu/workflows/49), a Galaxy-E workflow computing species presence/absence and community metrics from biodiversity data.

#### json
```json
{
  "name": "Population and community metrics calculation from Biodiversity data",
  "description": "Galaxy-E (ecology.usegalaxy.eu) workflow to calculate species presence / absence, community metrics and compute generalized linear models to identify effects and significativity of these effects on biodiversity.",
  "url": "https://workflowhub.eu/workflows/49",
  "keywords": "GLM, Species abundance, Community_metrics, Ecology, Modeling, Presence_absence, Biodiversity, Statistics",
  "license": "https://opensource.org/licenses/MIT",
  "creator": [
    {
      "name": "Yvan Le Bras",
      "url": "https://workflowhub.eu/people/51"
    },
    {
      "name": "Coline Royaux",
      "url": "https://workflowhub.eu/people/52"
    }
  ],
  "producer": [
    {
      "name": "PNDB",
      "url": "https://workflowhub.eu/projects/19"
    }
  ],
  "dateCreated": "2020-07-24",
  "dateModified": "2020-07-24",
  "encodingFormat": "application/zip",
  "sdPublisher": [
    {
      "name": "Yvan Le Bras",
      "url": "https://workflowhub.eu/people/51"
    }
  ],
  "version": 2,
  "image": "https://workflowhub.eu/workflows/49/diagram?version=2",
  "programmingLanguage": "Galaxy",
  "input": [
    {
      "name": "0_Input",
      "encodingFormat": "http://edamontology.org/format_3752",
      "additionalType": "http://edamontology.org/data_3707",
      "description": "Species count. A tabular file with observation data. Must at least contain three columns 'observation.unit' which associate year and location (alternatively, you can have this column split in 2 columns named 'year' and 'location'), 'species.code' with species ID and 'number' for abundance."
    }
  ],
  "output": []
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/bioschemas/computational-workflow/context.jsonld",
  "name": "Population and community metrics calculation from Biodiversity data",
  "description": "Galaxy-E (ecology.usegalaxy.eu) workflow to calculate species presence / absence, community metrics and compute generalized linear models to identify effects and significativity of these effects on biodiversity.",
  "url": "https://workflowhub.eu/workflows/49",
  "keywords": "GLM, Species abundance, Community_metrics, Ecology, Modeling, Presence_absence, Biodiversity, Statistics",
  "license": "https://opensource.org/licenses/MIT",
  "creator": [
    {
      "name": "Yvan Le Bras",
      "url": "https://workflowhub.eu/people/51"
    },
    {
      "name": "Coline Royaux",
      "url": "https://workflowhub.eu/people/52"
    }
  ],
  "producer": [
    {
      "name": "PNDB",
      "url": "https://workflowhub.eu/projects/19"
    }
  ],
  "dateCreated": "2020-07-24",
  "dateModified": "2020-07-24",
  "encodingFormat": "application/zip",
  "sdPublisher": [
    {
      "name": "Yvan Le Bras",
      "url": "https://workflowhub.eu/people/51"
    }
  ],
  "version": 2,
  "image": "https://workflowhub.eu/workflows/49/diagram?version=2",
  "programmingLanguage": "Galaxy",
  "input": [
    {
      "name": "0_Input",
      "encodingFormat": "http://edamontology.org/format_3752",
      "additionalType": "http://edamontology.org/data_3707",
      "description": "Species count. A tabular file with observation data. Must at least contain three columns 'observation.unit' which associate year and location (alternatively, you can have this column split in 2 columns named 'year' and 'location'), 'species.code' with species ID and 'number' for abundance."
    }
  ],
  "output": []
}
```

#### ttl
```ttl
@prefix bioschemas: <https://bioschemas.org/terms/> .
@prefix schema1: <http://schema.org/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] schema1:creator [ schema1:name "Coline Royaux" ;
            schema1:url "https://workflowhub.eu/people/52" ],
        [ schema1:name "Yvan Le Bras" ;
            schema1:url "https://workflowhub.eu/people/51" ] ;
    schema1:dateCreated "2020-07-24" ;
    schema1:dateModified "2020-07-24" ;
    schema1:description "Galaxy-E (ecology.usegalaxy.eu) workflow to calculate species presence / absence, community metrics and compute generalized linear models to identify effects and significativity of these effects on biodiversity." ;
    schema1:encodingFormat "application/zip" ;
    schema1:image "https://workflowhub.eu/workflows/49/diagram?version=2" ;
    schema1:keywords "GLM, Species abundance, Community_metrics, Ecology, Modeling, Presence_absence, Biodiversity, Statistics" ;
    schema1:license "https://opensource.org/licenses/MIT" ;
    schema1:name "Population and community metrics calculation from Biodiversity data" ;
    schema1:producer [ schema1:name "PNDB" ;
            schema1:url "https://workflowhub.eu/projects/19" ] ;
    schema1:programmingLanguage "Galaxy" ;
    schema1:sdPublisher [ schema1:name "Yvan Le Bras" ;
            schema1:url "https://workflowhub.eu/people/51" ] ;
    schema1:url "https://workflowhub.eu/workflows/49" ;
    schema1:version 2 ;
    bioschemas:input [ schema1:additionalType "http://edamontology.org/data_3707" ;
            schema1:description "Species count. A tabular file with observation data. Must at least contain three columns 'observation.unit' which associate year and location (alternatively, you can have this column split in 2 columns named 'year' and 'location'), 'species.code' with species ID and 'number' for abundance." ;
            schema1:encodingFormat "http://edamontology.org/format_3752" ;
            schema1:name "0_Input" ] .


```

## Schema

```yaml
$schema: https://json-schema.org/draft/2020-12/schema
title: Bioschemas ComputationalWorkflow
description: An orchestrated and repeatable pattern of activity, executed by a computational
  process, per the Bioschemas [ComputationalWorkflow](https://bioschemas.org/profiles/ComputationalWorkflow/1.0-RELEASE)
  profile.
type: object
required:
- input
- output
- programmingLanguage
- name
- url
- creator
- dateCreated
- license
- sdPublisher
- version
properties:
  input:
    description: An input required to use the computational workflow (e.g. an Excel
      spreadsheet, a BAM file).
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/bioschemas/formal-parameter/schema.yaml
    - type: array
      items:
        $ref: https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/bioschemas/formal-parameter/schema.yaml
    x-jsonld-id: https://bioschemas.org/terms/input
  output:
    description: An output produced by the workflow.
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/bioschemas/formal-parameter/schema.yaml
    - type: array
      items:
        $ref: https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/bioschemas/formal-parameter/schema.yaml
    x-jsonld-id: https://bioschemas.org/terms/output
  creativeWorkStatus:
    description: The status of the workflow in terms of its stage in a lifecycle,
      e.g. Incomplete, Draft, Published, Obsolete.
    anyOf:
    - type: string
    - type: array
      items:
        type: string
    - $ref: '#/$defs/definedTerm'
    - type: array
      items:
        $ref: '#/$defs/definedTerm'
    x-jsonld-id: http://schema.org/creativeWorkStatus
  documentation:
    description: Documentation describing the ComputationalWorkflow and its use.
    anyOf:
    - type: string
      format: uri
    - type: array
      items:
        type: string
        format: uri
    - $ref: '#/$defs/creativeWork'
    - type: array
      items:
        $ref: '#/$defs/creativeWork'
    x-jsonld-id: http://schema.org/documentation
  funding:
    description: The funding for the workflow.
    oneOf:
    - $ref: '#/$defs/grant'
    - type: array
      items:
        $ref: '#/$defs/grant'
    x-jsonld-id: http://schema.org/funding
  maintainer:
    description: The Person or Organization that manages contributions to, and/or
      publication of, the workflow.
    anyOf:
    - $ref: '#/$defs/person'
    - type: array
      items:
        $ref: '#/$defs/person'
    - $ref: '#/$defs/organization'
    - type: array
      items:
        $ref: '#/$defs/organization'
    x-jsonld-id: http://schema.org/maintainer
  softwareRequirements:
    description: Component dependency requirements for the workflow (runtime environments,
      shared libraries not bundled with it).
    anyOf:
    - type: string
      format: uri
    - type: array
      items:
        type: string
        format: uri
    - type: string
    - type: array
      items:
        type: string
    x-jsonld-id: http://schema.org/softwareRequirements
  conditionsOfAccess:
    description: Conditions that affect the availability of, or method(s) of access
      to, the workflow.
    type: string
    x-jsonld-id: http://schema.org/conditionsOfAccess
  targetProduct:
    description: Target operating system(s) / product(s) to which the workflow applies.
    oneOf:
    - $ref: '#/$defs/softwareApplication'
    - type: array
      items:
        $ref: '#/$defs/softwareApplication'
    x-jsonld-id: http://schema.org/targetProduct
  programmingLanguage:
    description: The computer programming (or workflow) language.
    anyOf:
    - type: string
    - type: array
      items:
        type: string
    - $ref: '#/$defs/computerLanguage'
    - type: array
      items:
        $ref: '#/$defs/computerLanguage'
    x-jsonld-id: http://schema.org/programmingLanguage
  runtimePlatform:
    description: Runtime platform or script interpreter dependencies (e.g. Java 1,
      Python 2.3).
    oneOf:
    - type: string
    - type: array
      items:
        type: string
    x-jsonld-id: http://schema.org/runtimePlatform
  alternateName:
    description: An alias for the workflow.
    oneOf:
    - type: string
    - type: array
      items:
        type: string
    x-jsonld-id: http://schema.org/alternateName
  description:
    description: A description of the workflow.
    type: string
    x-jsonld-id: http://schema.org/description
  identifier:
    description: Any kind of identifier for the workflow (e.g. an ISBN, GTIN, or UUID).
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
  image:
    description: An image of the workflow.
    oneOf:
    - type: string
      format: uri
    - type: array
      items:
        type: string
        format: uri
    - $ref: '#/$defs/imageObject'
    - type: array
      items:
        $ref: '#/$defs/imageObject'
    x-jsonld-id: http://schema.org/image
  name:
    description: The name of the workflow.
    type: string
    x-jsonld-id: http://schema.org/name
  url:
    description: URL of the workflow.
    type: string
    format: uri
    x-jsonld-id: http://schema.org/url
  citation:
    description: A citation or reference to another creative work related to the workflow.
    anyOf:
    - type: string
    - type: array
      items:
        type: string
    - $ref: '#/$defs/creativeWork'
    - type: array
      items:
        $ref: '#/$defs/creativeWork'
    x-jsonld-id: http://schema.org/citation
  contributor:
    description: A secondary contributor to the workflow.
    anyOf:
    - $ref: '#/$defs/person'
    - type: array
      items:
        $ref: '#/$defs/person'
    - $ref: '#/$defs/organization'
    - type: array
      items:
        $ref: '#/$defs/organization'
    x-jsonld-id: http://schema.org/contributor
  creator:
    description: The creator/author of the workflow.
    anyOf:
    - $ref: '#/$defs/person'
    - type: array
      items:
        $ref: '#/$defs/person'
    - $ref: '#/$defs/organization'
    - type: array
      items:
        $ref: '#/$defs/organization'
    x-jsonld-id: http://schema.org/creator
  dateCreated:
    description: The date on which the workflow was created.
    type: string
    format: date
    x-jsonld-id: http://schema.org/dateCreated
  dateModified:
    description: The date on which the workflow was most recently modified.
    type: string
    format: date
    x-jsonld-id: http://schema.org/dateModified
  datePublished:
    description: Date of first publication of the workflow.
    type: string
    format: date
    x-jsonld-id: http://schema.org/datePublished
  encodingFormat:
    description: Media type of the workflow, typically expressed as a MIME type (e.g.
      `application/zip`).
    anyOf:
    - type: string
      format: uri
    - type: array
      items:
        type: string
        format: uri
    - type: string
    - type: array
      items:
        type: string
    x-jsonld-id: http://schema.org/encodingFormat
  hasPart:
    description: A resource that is part of the workflow.
    oneOf:
    - $ref: '#/$defs/creativeWork'
    - type: array
      items:
        $ref: '#/$defs/creativeWork'
    x-jsonld-id: http://schema.org/hasPart
  isBasedOn:
    description: A resource from which the workflow is derived, or of which it is
      a modification.
    oneOf:
    - $ref: '#/$defs/product'
    - $ref: '#/$defs/creativeWork'
    - type: string
      format: uri
    x-jsonld-id: http://schema.org/isBasedOn
  keywords:
    description: Keywords or tags describing the workflow.
    oneOf:
    - type: string
    - type: array
      items:
        type: string
    x-jsonld-id: http://schema.org/keywords
  license:
    description: A license document that applies to the workflow, typically indicated
      by URL.
    anyOf:
    - type: string
      format: uri
    - type: array
      items:
        type: string
        format: uri
    - $ref: '#/$defs/creativeWork'
    - type: array
      items:
        $ref: '#/$defs/creativeWork'
    x-jsonld-id: http://schema.org/license
  producer:
    description: The person or organization who produced the workflow.
    anyOf:
    - $ref: '#/$defs/person'
    - type: array
      items:
        $ref: '#/$defs/person'
    - $ref: '#/$defs/organization'
    - type: array
      items:
        $ref: '#/$defs/organization'
    x-jsonld-id: http://schema.org/producer
  publisher:
    description: The publisher of the workflow.
    anyOf:
    - $ref: '#/$defs/person'
    - type: array
      items:
        $ref: '#/$defs/person'
    - $ref: '#/$defs/organization'
    - type: array
      items:
        $ref: '#/$defs/organization'
    x-jsonld-id: http://schema.org/publisher
  sdPublisher:
    description: The party responsible for generating and publishing the current structured
      data markup for the workflow.
    anyOf:
    - $ref: '#/$defs/person'
    - type: array
      items:
        $ref: '#/$defs/person'
    - $ref: '#/$defs/organization'
    - type: array
      items:
        $ref: '#/$defs/organization'
    x-jsonld-id: http://schema.org/sdPublisher
  version:
    description: The version of the workflow.
    oneOf:
    - type: string
    - type: number
    x-jsonld-id: http://schema.org/version
$defs:
  grant:
    type: object
    required:
    - name
    properties:
      name:
        type: string
        x-jsonld-id: http://schema.org/name
      url:
        type: string
        format: uri
        x-jsonld-id: http://schema.org/url
      sponsor:
        oneOf:
        - $ref: '#/$defs/organization'
        - $ref: '#/$defs/person'
        x-jsonld-id: http://schema.org/sponsor
      identifier:
        type: string
        x-jsonld-id: http://schema.org/identifier
  person:
    type: object
    required:
    - name
    properties:
      name:
        type: string
        x-jsonld-id: http://schema.org/name
      url:
        type: string
        format: uri
        x-jsonld-id: http://schema.org/url
      affiliation:
        $ref: '#/$defs/organization'
        x-jsonld-id: http://schema.org/affiliation
  organization:
    type: object
    properties:
      name:
        type: string
        x-jsonld-id: http://schema.org/name
      alternateName:
        type: string
        x-jsonld-id: http://schema.org/alternateName
      identifier:
        type: string
        x-jsonld-id: http://schema.org/identifier
      url:
        type: string
        format: uri
        x-jsonld-id: http://schema.org/url
  softwareApplication:
    type: object
    properties:
      name:
        type: string
        x-jsonld-id: http://schema.org/name
      url:
        type: string
        format: uri
        x-jsonld-id: http://schema.org/url
  propertyValue:
    type: object
    required:
    - name
    - value
    properties:
      name:
        type: string
        x-jsonld-id: http://schema.org/name
      value:
        oneOf:
        - type: string
        - type: boolean
        - type: number
        x-jsonld-id: http://schema.org/value
      identifier:
        type: string
        x-jsonld-id: http://schema.org/identifier
      valueReference:
        oneOf:
        - $ref: '#/$defs/categoryCode'
        - type: array
          items:
            $ref: '#/$defs/categoryCode'
        x-jsonld-id: http://schema.org/valueReference
      unitCode:
        anyOf:
        - type: string
        - type: string
          format: uri
        x-jsonld-id: http://schema.org/unitCode
      unitText:
        type: string
        x-jsonld-id: http://schema.org/unitText
  categoryCode:
    type: object
    required:
    - name
    - codeValue
    - url
    properties:
      name:
        type: string
        x-jsonld-id: http://schema.org/name
      codeValue:
        type: string
        x-jsonld-id: http://schema.org/codeValue
      url:
        type: string
        x-jsonld-id: http://schema.org/url
  creativeWork:
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
  product:
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
  definedTerm:
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
      termCode:
        type: string
        x-jsonld-id: http://schema.org/termCode
  computerLanguage:
    type: object
    properties:
      name:
        type: string
        x-jsonld-id: http://schema.org/name
  imageObject:
    type: object
    properties:
      name:
        type: string
        x-jsonld-id: http://schema.org/name
      url:
        type: string
        format: uri
        x-jsonld-id: http://schema.org/url
x-jsonld-extra-terms:
  ComputationalWorkflow: https://bioschemas.org/terms/ComputationalWorkflow
  codeValue: http://schema.org/codeValue
x-jsonld-prefixes:
  bioschemas: https://bioschemas.org/terms/
  schema: http://schema.org/

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/bioschemas/computational-workflow/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/bioschemas/computational-workflow/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "ComputationalWorkflow": "bioschemas:ComputationalWorkflow",
    "codeValue": "schema:codeValue",
    "input": {
      "@context": {
        "identifier": {
          "@context": {
            "propertyID": "schema:propertyID"
          },
          "@id": "schema:identifier"
        },
        "additionalType": "schema:additionalType",
        "defaultValue": "schema:defaultValue",
        "valueRequired": "schema:valueRequired"
      },
      "@id": "bioschemas:input"
    },
    "output": {
      "@context": {
        "identifier": {
          "@context": {
            "propertyID": "schema:propertyID"
          },
          "@id": "schema:identifier"
        },
        "additionalType": "schema:additionalType",
        "defaultValue": "schema:defaultValue",
        "valueRequired": "schema:valueRequired"
      },
      "@id": "bioschemas:output"
    },
    "creativeWorkStatus": {
      "@context": {
        "termCode": "schema:termCode"
      },
      "@id": "schema:creativeWorkStatus"
    },
    "documentation": "schema:documentation",
    "funding": {
      "@context": {
        "sponsor": {
          "@context": {
            "affiliation": "schema:affiliation"
          },
          "@id": "schema:sponsor"
        }
      },
      "@id": "schema:funding"
    },
    "maintainer": {
      "@context": {
        "affiliation": "schema:affiliation"
      },
      "@id": "schema:maintainer"
    },
    "softwareRequirements": "schema:softwareRequirements",
    "conditionsOfAccess": "schema:conditionsOfAccess",
    "targetProduct": "schema:targetProduct",
    "programmingLanguage": "schema:programmingLanguage",
    "runtimePlatform": "schema:runtimePlatform",
    "alternateName": "schema:alternateName",
    "description": "schema:description",
    "identifier": {
      "@context": {
        "value": "schema:value",
        "valueReference": "schema:valueReference",
        "unitCode": "schema:unitCode",
        "unitText": "schema:unitText"
      },
      "@id": "schema:identifier"
    },
    "image": "schema:image",
    "name": "schema:name",
    "url": "schema:url",
    "citation": "schema:citation",
    "contributor": {
      "@context": {
        "affiliation": "schema:affiliation"
      },
      "@id": "schema:contributor"
    },
    "creator": {
      "@context": {
        "affiliation": "schema:affiliation"
      },
      "@id": "schema:creator"
    },
    "dateCreated": "schema:dateCreated",
    "dateModified": "schema:dateModified",
    "datePublished": "schema:datePublished",
    "encodingFormat": "schema:encodingFormat",
    "hasPart": "schema:hasPart",
    "isBasedOn": "schema:isBasedOn",
    "keywords": "schema:keywords",
    "license": "schema:license",
    "producer": {
      "@context": {
        "affiliation": "schema:affiliation"
      },
      "@id": "schema:producer"
    },
    "publisher": {
      "@context": {
        "affiliation": "schema:affiliation"
      },
      "@id": "schema:publisher"
    },
    "sdPublisher": {
      "@context": {
        "affiliation": "schema:affiliation"
      },
      "@id": "schema:sdPublisher"
    },
    "version": "schema:version",
    "FormalParameter": "bioschemas:FormalParameter",
    "bioschemas": "https://bioschemas.org/terms/",
    "schema": "http://schema.org/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-ro-crate/build/annotated/researchobject/ro-crate/bioschemas/computational-workflow/context.jsonld)

## Sources

* [Bioschemas ComputationalWorkflow profile 1.0-RELEASE](https://bioschemas.org/profiles/ComputationalWorkflow/1.0-RELEASE)
* [RO-Crate Workflow profile](https://www.researchobject.org/ro-crate/specification/1.3/workflows.html)

# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-ro-crate](https://github.com/ogcincubator/bblocks-ro-crate)
* Path: `_sources/bioschemas/computational-workflow`

