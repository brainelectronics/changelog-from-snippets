# Changelog from Snippets Action

[![Create release](https://github.com/brainelectronics/changelog-from-snippets/actions/workflows/release.yaml/badge.svg)](https://github.com/brainelectronics/changelog-from-snippets/actions/workflows/release.yaml)
![Release](https://img.shields.io/github/v/release/brainelectronics/changelog-from-snippets?include_prereleases&color=success)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

GitHub Action for creating changelogs based on snippets

---

<!-- MarkdownTOC -->

- [Requirements](#requirements)
- [Usage](#usage)
  - [Basic usage](#basic-usage)
  - [Customizing](#customizing)
- [License](#license)

<!-- /MarkdownTOC -->

## Requirements

As this Action uses [snippets2changelog](https://github.com/brainelectronics/snippets2changelog)
to generate a changelog based on individual snippets, the requirements for the
changelog format have to meet certain criterias.

## Usage

### Basic usage

With the default values used a changelog named `changelog.md` file located in
the project root will be parsed and the new changelog will be created as
`changelog.md.new` at the same location. For further details check the
[customizing section](#customizing)

See [action.yml](action.yml)

```yaml
name: Create changelog

on:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  release:
    runs-on: ubuntu-latest
    name: Changelog
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          # all history is needed to crawl it properly
          fetch-depth: 0
      - name: 'Create changelog based on snippets'
        uses: brainelectronics/changelog-from-snippets@v1
```

**Ensure the `fetch-depth` option value is set to `0` during the checkout**

### Customizing

The following are optional as `step.with` keys

| Name                      | Type    | Description                                              |
| ------------------------- | ------- | ---------------------------------------------------------|
| `changelog-path`          | String  | Path to (existing) changelog. Default to `changelog.md`  |
| `snippets-path`           | String  | Path to folder with snippets. Default to `.snippets`     |
| `update-in-place`         | Boolean | Update changelog in place. Defaults to `false`           |
| `skip-internal`           | Boolean | Skip snippets with scope `internal`. Defaults to `false` |

```yaml
steps:
  - name: Checkout
    uses: actions/checkout@v4
  - name: 'Create changelog based on snippets'
    uses: brainelectronics/changelog-from-snippets@v1
    with:
      changelog-path: path/to/changelog.md
      changelog-path: path/to/snippets/
      update-in-place: true
      skip-internal: true
```

## License

The scripts and documentation in this project are released under the
[MIT License](LICENSE)
