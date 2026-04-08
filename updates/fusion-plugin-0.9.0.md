---
description: Posted 2026/04/08
---

# Fusion Plugin v0.9.0 Beta

This is the first **beta** release of the [Carvera Community Fusion 360 plugin](fusion/plugin.md). This plugin helps users of personal edition Fusion 360 generate G-code files with features similar to those found in the Professional Fusion 360 edition.

Download the v0.9.0 Beta release from [GitHub](https://github.com/Carvera-Community/Carvera_Community_FusionPlugin/releases/tag/v0.9.0-beta.1)

## Highlights

- **Indexed 4th axis support**:
  - Automatic rotation of **A-axis between setups**
  - optional **Y-axis retract** before rotation (in addition to Z retract)
  - configurable **Y retract position using G53/MCS**
- **Rapid movement**: converts normally slow non-cutting moves, to G0 rapids based on a number of configurable options such as minimum-distance strategy.
- **Flexible output organization**:
  - grouping: **single file**, **per setup**, **per setup + tool**, or **per operation**
  - options for numeric-only program names, sequence numbering, flattening folders, overwrite protection, and clearing the output folder before generating
- **Utilities**: batch setup renaming (supports regex), and per-document settings with saved defaults.

## Beta note / feedback

Please note that this is the first release of this plugin and there may be bugs. Please report issues via [GitHub issues](https://github.com/Carvera-Community/Carvera_Community_FusionPlugin/issues) or the community Discord channels linked in the full docs: `fusion/plugin.md`.
