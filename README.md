# BornInTeyvat Public Dataset

A small, machine-readable dataset of Genshin Impact character birthdays, elements, nations, and rarities, maintained as the public data companion to the **Born in Teyvat** project.

Current dataset version: **1.0.0** (6 November 2026).

This repository contains **data and documentation only**. It does not contain the Born in Teyvat website source code, React components, TypeScript application logic, CSS, UI, design, routing, configuration, avatars, or artwork.

> Born in Teyvat is an unofficial fan-made project and is not affiliated with, endorsed by, or sponsored by HoYoverse. Genshin Impact and related intellectual property belong to their respective owners.

## Contents

| File | Records | Description |
|---|---:|---|
| `data/characters.json` | 122 | Character birthday, element, nation, and rarity records |
| `data/nations.json` | 8 | Nation identifiers, names, and associated elements |
| `schema/characters.schema.json` | — | JSON Schema 2020-12 for the character dataset |
| `schema/nations.schema.json` | — | JSON Schema 2020-12 for the nation dataset |
| `DATA-LICENSE.md` | — | Limited CC BY 4.0 scope and exclusions |
| `THIRD-PARTY-NOTICES.md` | — | Source attribution and third-party rights |
| `CONTRIBUTING.md` | — | Contribution and source requirements |
| `CHANGELOG.md` | — | Dataset revisions |

## Repository layout

```text
BornInTeyvat-public/
|-- data/
|   |-- characters.json
|   `-- nations.json
|-- schema/
|   |-- characters.schema.json
|   `-- nations.schema.json
|-- README.md
|-- DATA-LICENSE.md
|-- THIRD-PARTY-NOTICES.md
|-- CONTRIBUTING.md
`-- CHANGELOG.md
```

## JSON structure

### Characters

`data/characters.json` is an array of objects with exactly these fields:

```json
[
  {
    "id": "amber",
    "name": "Amber",
    "birthday": "08-10",
    "element": "Pyro",
    "nation": "Mondstadt",
    "rarity": 4
  }
]
```

This example illustrates the schema only. It is not a separate confirmation that every field has been legally cleared; see `DATA-LICENSE.md`.

### Nations

`data/nations.json` is an array of objects with these fields:

```json
[
  {
    "id": "mondstadt",
    "name": "Mondstadt",
    "element": "Anemo"
  },
  {
    "id": "nodkrai",
    "name": "Nod-Krai"
  }
]
```

The `element` field is optional because not every nation has a published associated element. At present, Nod-Krai has no `element` value.

## Field definitions

### Character fields

| Field | Type | Required | Description |
|---|---|:---:|---|
| `id` | string | Yes | Stable kebab-case identifier, for example `lan-yan`. Must not change once published. |
| `name` | string | Yes | Character display name. |
| `birthday` | string | Yes | Month and day in `MM-DD` format. February 29 is preserved. |
| `element` | string | Yes | One of `Anemo`, `Cryo`, `Dendro`, `Electro`, `Geo`, `Hydro`, `Pyro`. |
| `nation` | string | Yes | One of `Fontaine`, `Inazuma`, `Liyue`, `Mondstadt`, `Natlan`, `Nod-Krai`, `Other`, `Snezhnaya`, `Sumeru`. |
| `rarity` | integer | Yes | `4` or `5`, representing stars. |

### Nation fields

| Field | Type | Required | Description |
|---|---|:---:|---|
| `id` | string | Yes | Stable kebab-case identifier, for example `nodkrai`. Must not change once published. |
| `name` | string | Yes | Nation display name. |
| `element` | string | No | Associated element, using the same values as the character `element` field. |

### Nation classification

`Other` is a valid character `nation` classification, not a nation record. It is used for characters who do not have a matching record in `data/nations.json`. The nation dataset therefore contains 8 records while the character dataset uses 9 possible `nation` values including `Other`.

## Date format

Birthdays use `MM-DD`, zero-padded, with no year:

- January 3 is `01-03`.
- August 10 is `08-10`.
- February 29 is `02-29` and is valid.

Birthdays are anniversaries, not full dates. Consumers should not assume a year and should decide how to handle February 29 in non-leap years.

## Data sources and provenance

The records were compiled for the Born in Teyvat project and cross-checked against community and reference sources, including:

- Game8
- Genshin Impact Wiki
- Yatta / Project Amber
- Enka.Network
- HoYoWiki

These sources are credited for reference and verification. **Attribution does not grant permission to redistribute third-party database contents.** The project owner cannot relicense material owned by others and does not claim ownership of Genshin Impact intellectual property. See `THIRD-PARTY-NOTICES.md` for details and unresolved questions.

Only the fields documented above are part of this repository. Character avatars, PNG files, artwork, logos, constellation text, descriptive text, inspiration text, and website metadata are intentionally excluded.

## Licensing scope

The two JSON files in `data/` are made available under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**, to the extent the project owner holds the relevant rights:

- https://creativecommons.org/licenses/by/4.0/
- https://creativecommons.org/licenses/by/4.0/legalcode

The license covers only `data/characters.json` and `data/nations.json`, limited to the fields documented in this README. It does not cover the repository as a whole, the Born in Teyvat website implementation, images, trademarks, or third-party material.

There is intentionally no root `LICENSE` file that could be mistaken for a repository-wide license.

If you redistribute the data or a modified version, provide attribution, link to the license, link to this repository where reasonably practicable, and indicate what you changed. Suggested attribution:

> Character and nation data from the BornInTeyvat Public Dataset by CheemsGalaxy, licensed under CC BY 4.0.
> Source: https://github.com/CheemsGalaxy/BornInTeyvat-public
> License: https://creativecommons.org/licenses/by/4.0/
> Changes: [describe your changes]

This summary is not legal advice and does not replace the license text.

## Third-party exclusions

The following are not licensed by this repository:

- Genshin Impact characters, names, elements, nations, artwork, logos, and related trademarks, which belong to COGNOSPHERE PTE. LTD. (HoYoverse) and their respective owners.
- Any database, table, text, or image obtained from Game8, Genshin Impact Wiki, Yatta / Project Amber, Enka.Network, or HoYoWiki.
- The Born in Teyvat website source code, UI, design, and visual assets.
- Character avatars, character PNG files, and any other artwork.

No images are distributed in this repository. The absence of an image is intentional.

## Usage examples

Fetch the datasets directly from GitHub:

```js
const base =
  "https://raw.githubusercontent.com/CheemsGalaxy/BornInTeyvat-public/main";

const characters = await fetch(`${base}/data/characters.json`).then((response) => {
  if (!response.ok) throw new Error(`HTTP ${response.status}`);
  return response.json();
});

const nations = await fetch(`${base}/data/nations.json`).then((response) => {
  if (!response.ok) throw new Error(`HTTP ${response.status}`);
  return response.json();
});

const mondstadtCharacters = characters.filter(
  (character) => character.nation === "Mondstadt",
);
```

With `curl` and `jq`:

```sh
curl -fsSL https://raw.githubusercontent.com/CheemsGalaxy/BornInTeyvat-public/main/data/characters.json \
  | jq '[.[] | select(.element == "Pyro") | {name, birthday}]'
```

Pin to a release tag or commit when reproducibility matters. `main` can change as records are corrected or added.

## Validation

The JSON files must parse as valid UTF-8 JSON and conform to the schemas in `schema/`. Before contributing, validate both files with a JSON Schema 2020-12 validator and check that:

- every `id` is unique;
- every required field is present and non-empty;
- every birthday matches `MM-DD` and is a real calendar day;
- every `element`, `nation`, and `rarity` value is in the documented set;
- every character `nation` is either present in `data/nations.json` or is `Other`.

## Contributing

Corrections and additions are welcome when they can be verified. Read `CONTRIBUTING.md` before opening a pull request. Do not submit website source code, artwork, or third-party database dumps.

Contributions are not automatically treated as licensed under CC BY 4.0. A contribution is accepted under that license only after the contributor explicitly agrees and confirms they have the rights needed to license it.

## Disclaimer

Born in Teyvat is an unofficial fan-made project and is not affiliated with, endorsed by, or sponsored by HoYoverse. Genshin Impact and related intellectual property belong to their respective owners.

The dataset is provided "as is", without warranties of any kind, to the extent permitted by applicable law. The project owner does not claim legal clearance for third-party material and cannot grant rights they do not hold.
