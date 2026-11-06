# Changelog

All notable changes to the BornInTeyvat Public Dataset are documented in this file.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/). Dataset versions are separate from the private Born in Teyvat website's versions.

## [Unreleased]

## [1.0.0] - 2026-11-06

### Added

- Initial public dataset release.
- `data/characters.json` with 122 character records.
- `data/nations.json` with 8 nation records.
- JSON Schema 2020-12 definitions for both datasets.
- Documentation for field definitions, date format, attribution, licensing scope, third-party exclusions, and contribution requirements.

### Changed

- Normalized character birthdays from source month/day objects to zero-padded `MM-DD` strings.
- Normalized element and nation values to display names.
- Kept stable kebab-case identifiers from the source records.

### Excluded

- Character constellations, avatars, and artwork.
- Nation `inspiration` text.
- Website source code, React components, TypeScript application logic, CSS, UI, routing, and configuration.
- Third-party text, images, and database exports.

### Notes

- `Other` is a character nation classification, not a nation record.
- Nod-Krai has no published `element` value in this release.
- The licensing scope is limited to the two JSON files and the fields documented in `DATA-LICENSE.md`. No root `LICENSE` is provided.
