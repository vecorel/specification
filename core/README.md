# Core Specification <!-- omit in toc -->

This specification describes the core data and metadata properties that describe a Vecorel Feature.
The specification doesn't distinguish between collection-level and feature-level properties,
common definitions are shared across these levels.

- A Collection refers to a group of one or more features.
- A Feature is a single field geometry with additional properties.

- **Schema:** <https://vecorel.github.io/specification/v0.1.0/schema.yaml>

## Table of Contents <!-- omit in toc -->

- [General Properties](#general-properties)
  - [schemas](#schemas)
  - [id](#id)
  - [collection](#collection)
- [Spatial Properties](#spatial-properties)
- [Schema Language](#schema-language)

## General Properties

| Property Name | Data Type                       | Description |
| ------------- | ------------------------------- | ----------- |
| schemas       | object\<string, array\<string>> | **REQUIRED.** A list of schemas the collection implements. |
| id            | string                          | **REQUIRED.** An identifier for the entity. |
| collection    | string                          | **REQUIRED.** The identifier of the collection. |

### schemas

The schemas the collection implements.
Each schema must be a valid HTTP(S) URLs to an existing YAML files compliant to Vecorel SDL.
The schema for this specification (see above) is required to be provided.

Each `collection` must have a single set of applicable schemas.
The key of the dictionary must be equal to the value provided for the `collection` property.

The schema URI for Vecorel that is listed above is required to be present.

**Example for `schemas`:**

This describes two collections `abc` and `xyz`.

```json
{
  "abc": [
    "https://vecorel.github.io/specification/v0.1.0/schema.yaml"
  ],
  "xyz": [
    "https://vecorel.github.io/specification/v0.1.0/schema.yaml",
    "https://vecorel.github.io/crop-extension/v0.1.0/schema.yaml",
  ]
}
```

### id

It must be unique per collection, i.e. `collection` and `id` form a unique identifier.

### collection

A collection is a group of one or more features with a unique identifier, stored in the `collection` property.

Encodings may support to store properties that consists of the same value across all features at the collection-level.
This de-duplicates data for more efficient resource usage, but only applies if more than two features are available for the collection.
The specific location and behaviour of collection-level data is specified in the encoding-specific specifications.

**Example:**

You have two different datasets named `abc` (CC-0 licensed) and `xyz` (CC-BY-4.0 licensed).
If you store the datasets separately, you can store the license in the collection-level data
as the value for the property is the same for all features.
Once you merged the two datasets, you must ensure that a unique identifier for the collection is provieded
(here: `abc` and `xyz`) so that IDs are unique.
Additionally, you have to add the license property on the feature-level as the licenses are now twofold.

## Spatial Properties

| Property Name | Data Type    | Description |
| ------------- | ------------ | ----------- |
| geometry      | geometry     | **REQUIRED.** A geometry that reflects the footprint of the described entity. Default CRS is WGS84. |
| bbox          | bounding-box | The bounding box of the geometry. |

## Schema Language

The schema language used for Vecorel is [Vecorel SDL](https://github.com/vecorel/sdl), version 0.2.0.

The data types in the tables above are defined in the document
[Data Types](https://github.com/vecorel/sdl/blob/v0.2.0/datatypes.md).

Vecorel SDL defines a (limited) set of data types and a
[vocabulary](https://github.com/vecorel/sdl/blob/v0.2.0/README.md#vocabulary)
to express additional constraints for these data types.
This allows to define a clear mapping between the core specification and its encodings.
