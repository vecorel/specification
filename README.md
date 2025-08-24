# Vector Core Language (Vecorel) Specification

The Vector Core Language (Vecorel) project is focused on making any kind of vector data (i.e. geospatial geometries with additional properties) openly available in a unified format on a global scale.
We believe that the Vecorel specification is a foundational aspect of vector data interoperability
which enables and accelerates additional layers of collaboration and detail via custom extensions.
This repository contains the core specification for Vecorel, including the data schema.
For more context, information on the ecosystem, and points of contact see the
[Vecorel GitHub organization](https://github.com/vecorel/).

- Version: **0.1.0**

> [!IMPORTANT]  
> The Vecorel specification is a work in progress.
> Feedback is welcome and encouraged.
> You can follow our [CHANGELOG](https://github.com/vecorel/specification/blob/main/CHANGELOG.md) to track our progress.

## Key Features

The center of Vecorel is the specification for representing vector data in GeoJSON & GeoParquet in a standard way,
with several optional extensions that specify additional attributes.
The core data schema of Vecorel is quite simple: it’s a set of definitions for attribute names and values.
The number of attributes in the core is quite small by design.
The idea is that most of the ‘interesting’ data about the property will be located in extensions.

The specification in this repository consists of three parts:

- [Core Specification](core/README.md)
  (file format agnostic definition for data and metadata)
- [GeoJSON Encoding](geojson/README.md)
- [GeoParquet Encoding](geoparquet/README.md)

To complement the specification, there are also best practices and extensions available:

- [Best Practices](best-practices/README.md)
- [Extensions](https://github.com/vecorel/extensions/)

## Relation to other standards and working groups

Vecorel doesn't aim to reinvent the wheel.
Our aim is to align with existing efforts as much as possible.

If you think we are missing relevant work here, we'd love to hear from you.
Please get in touch by [opening an issue](https://github.com/vecorel/specification/issues/new)!

## Contributing

The Vecorel community strives to provide a welcoming and transparent environment for all of the project’s participants.
You can find additional information about our community best practices and collaborative development processes below:
  
- [Code of Conduct](https://vecorel.org/code-of-conduct/)
- [Contribution Guideline](CONTRIBUTING.md)
- [Development and Release Process](process.md)
