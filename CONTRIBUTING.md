# Contributing

Thank you for helping improve the BornInTeyvat Public Dataset. This repository accepts **data corrections and additions only**. It does not accept website source code, UI, design, or artwork.

## Before you contribute

Read `README.md`, `DATA-LICENSE.md`, and `THIRD-PARTY-NOTICES.md`. By opening a pull request you confirm that you have read the licensing terms and can agree to them.

## What is accepted

- Corrections to a character's birthday, element, nation, or rarity.
- Corrections to a nation's name or associated element.
- New character records when the character is publicly released and the facts can be verified.
- Documentation fixes that do not change the meaning of the dataset.
- Schema fixes that do not silently break existing records.

## What is not accepted

- Website source code, React components, TypeScript application logic, CSS, UI, routing, or configuration.
- Character avatars, PNG files, artwork, logos, screenshots, or other images.
- Constellation names, lore text, character stories, voice lines, or other narrative game text.
- Third-party database dumps, scraped tables, or copied wiki pages.
- Generated data that is not backed by a verifiable source.
- Changes to existing stable `id` values.
- New fields that are not part of the documented schema.
- Reformatting that changes the meaning of a record.

## Data requirements

### Characters

Each record in `data/characters.json` must contain exactly:

```json
{
  "id": "amber",
  "name": "Amber",
  "birthday": "08-10",
  "element": "Pyro",
  "nation": "Mondstadt",
  "rarity": 4
}
```

- `id` is a stable lowercase kebab-case identifier. Do not change an existing ID. New IDs must match `^[a-z0-9]+(?:-[a-z0-9]+)*$`.
- `name` is the display name used by the dataset.
- `birthday` uses zero-padded `MM-DD`. February 29 is valid.
- `element` must be one of `Anemo`, `Cryo`, `Dendro`, `Electro`, `Geo`, `Hydro`, `Pyro`.
- `nation` must be one of `Fontaine`, `Inazuma`, `Liyue`, `Mondstadt`, `Natlan`, `Nod-Krai`, `Other`, `Snezhnaya`, `Sumeru`.
- `rarity` must be the integer `4` or `5`.
- No additional fields are allowed.

### Nations

Each record in `data/nations.json` must contain:

- `id`, using the same stable kebab-case rules;
- `name`;
- `element` only when an associated element is published, using the same values as character elements.

Do not add an `Other` record to `data/nations.json`. `Other` is a character classification only.

### Ordering

Keep `data/characters.json` ordered by `birthday` from `01-01` to `12-31`. Where birthdays tie, preserve the existing order. Insert a new record at the matching position instead of appending it to the end.

Keep `data/nations.json` in its existing canonical order unless a maintainer asks for a reordering.

## Source requirements

Every factual change needs a reliable source. In the pull request, include:

1. The exact record and field being changed.
2. The old value and the new value.
3. One or more source URLs.
4. The date you accessed each source.
5. A short explanation of why the source supports the change.

Prefer an official HoYoverse announcement, in-game data, or an official character page. Reputable community references may be used for cross-checking, but a source that merely copies this dataset is not independent verification.

Do not paste copyrighted text from a source into the pull request. Describe the fact in your own words.

If sources disagree, say so explicitly and do not guess. A record with unresolved conflicts should stay unchanged until a maintainer can review the evidence.

## Identifying uncertain information

Label uncertain claims clearly in the pull request description. Do not present a guess as verified data. If a value cannot be verified, leave the record unchanged or open an issue instead of a pull request.

Acceptable examples:

- "The source lists 08-10, but a second source lists 08-11. I did not change the file."
- "This character was announced but has no confirmed birthday. I am requesting guidance, not adding a record."

## Licensing of contributions

You retain copyright in your original contribution. This project does not claim ownership of your submission.

To keep the dataset consistently licensed, a contribution can be merged into `data/` only when you explicitly agree to license your contribution under **CC BY 4.0**, to the extent you hold the rights needed to do so, and confirm that:

- you created the contribution or have permission to submit it;
- you did not copy protected text, artwork, or a third-party database;
- you understand that factual material may also be subject to third-party rights;
- you grant the project and downstream users the rights described in `DATA-LICENSE.md`.

Include this statement in the pull request description:

> I license this contribution under CC BY 4.0. I confirm that I have the rights needed to do so and that I did not copy protected third-party text, images, or database contents.

A maintainer may ask for clarification before merging. Pull requests without an explicit license statement will not be merged into the licensed data files. Do not submit material if you cannot agree to these terms.

## Validation

Before opening a pull request:

1. Confirm both JSON files parse.
2. Validate them against `schema/characters.schema.json` and `schema/nations.schema.json` using a JSON Schema 2020-12 validator.
3. Confirm there are no duplicate `id` values.
4. Confirm every birthday is a real `MM-DD` date, including `02-29`.
5. Confirm every character `nation` exists in `data/nations.json` or is exactly `Other`.
6. Confirm the files remain UTF-8 and end with a newline.

A quick parse check with Node.js:

```sh
node -e "JSON.parse(require('fs').readFileSync('data/characters.json', 'utf8'))"
node -e "JSON.parse(require('fs').readFileSync('data/nations.json', 'utf8'))"
```

## Pull request process

1. Open a pull request with a clear title.
2. Describe the change and link the sources.
3. Include the license statement above.
4. Complete the validation steps.
5. Respond to review questions.

Maintainers may close a pull request that includes unverified data, copied material, artwork, or code. A closed pull request is not a judgment about the contributor; it means the change could not be accepted under the repository's licensing and data rules.

## Reporting a data concern

If you find an error but cannot provide a source, open an issue with the record ID, the field, the current value, and what you believe is correct. Clearly mark it as unverified.
