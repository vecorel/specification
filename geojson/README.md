# GeoJSON Encoding Specification

The GeoJSON encoding defines to encode vector data compliant to Vecorel as
GeoJSON as defined in [IETF RFC7946](https://datatracker.ietf.org/doc/html/rfc7946).

A single Vecorel Feature must be encoded as a GeoJSON [`Feature`](#feature).
Multiple Vecorel Features should be provided as a GeoJSON [`FeatureCollection`](#featurecollection).
Other GeoJSON types are not allowed.

Related documents:

- [Examples](examples/)
- [Datatype mapping](datatypes.md)

## Feature

- Example: [individual features](examples/individual-features/)

Each [Vecorel Feature](../core/README.md) must be a valid
[GeoJSON Feature](https://datatracker.ietf.org/doc/html/rfc7946#section-3.2).

The following properties are defined for a GeoJSON Feature (at the top-level of the object):

| Property Name | Data Type           | Description |
| ------------- | ------------------- | ----------- |
| id            | string              | **REQUIRED.** See [id](../core/README.md#id) in the core specification, must not be a `number` |
| type          | string              | **REQUIRED.** The GeoJSON type, must be: `Feature` |
| geometry      | object              | **REQUIRED.** A [GeoJSON Geometry Object](https://datatracker.ietf.org/doc/html/rfc7946#section-3.1), must not be `null` |
| bbox          | array\<number>      | A [GeoJSON Bounding Box](https://datatracker.ietf.org/doc/html/rfc7946#section-5) |
| properties    | object              | An object with all additional properties (see [`properties`](#properties)) |

The mapping between the Parquet data types and the Vecorel SDL data types, can be found in the
[data type mapping](datatypes.md).

> [!IMPORTANT]  
> RFC 7946 doesn't support a property named `crs`, which was only available in an earlier version of
> GeoJSON (2008).
> The CRS of the GeoJSON geometry and bbox must be WGS 84 / OGC CRS 84,
> see the [RFC 7946, chapter 4](https://datatracker.ietf.org/doc/html/rfc7946#section-4) for details.

For GeoJSON Features, collection-level data is only applicable for properties that are
collection-only, e.g. `schemas`.
All collection-level data is stored on the top-level of the Feature object as
[foreign members](https://datatracker.ietf.org/doc/html/rfc7946#section-6.1).
All other data is always in the [`properties`](#properties) as it's just a single entity and
there is no meaningful way to determine what collection-level data is.
This behaviour does not apply for GeoJSON Features within a GeoJSON FeatureCollection.

### properties

Must include any property that is required by the Vecorel specification.
May include any additional property.
All properties defined by the core specification or extensions should be provided here
except for `id`, `geometry`, `bbox` and collection-only properties.

## FeatureCollection

- Example: [a feature collection](examples/featurecollection/features.json)

All features in a GeoJSON FeatureCollection must be Vecorel-compliant.

Properties can also be stored at the [collection-level](../core/README.md#collection)
if all values for a specific property have the same value in all features.
This de-duplicates data for more efficient resource usage.
All properties are stored on the top-level of the FeatureCollection object as
[foreign members](https://datatracker.ietf.org/doc/html/rfc7946#section-6.1).
The individual features shall not contain any properties that are stored at the collection-level.
Validation must ensure that the collection-level properties are taken into account.
The de-duplication means that the individual features may not be valid without prior hydration
(i.e. moving the collection-level properties back into the Feature properties).

The following properties in Features can't be collection-level properties:

- `id`
- `geometry`
- `bbox`

Properties with the following names can#t be moved to the collection-level due to conflicts with the
FeatureCollection properties defined by GeoJSON:

- `features`
- `type`
