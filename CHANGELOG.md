# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Rules for merging collections

### Changed

- Clarified that collection-level data applies to all features, except for `schemas`

### Fixed

- The GeoParquet bit width of `uint32` is 32
- Collection-level data can be used with at least two features (was: more than two)
- Various typos and an invalid JSON example

## [v0.1.0] - 2025-08-15

- First release

[Unreleased]: <https://github.com/vecorel/specification/compare/v0.1.0...main>
[v0.1.0]: <https://github.com/vecorel/specification/tree/v0.1.0>
