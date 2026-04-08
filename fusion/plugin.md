# Fusion Plugin
{% hint style="warning" %}
This plugin is currently in beta. You may encounter bugs or unexpected behavior. Please report issues in the GitHub [issues section](https://github.com/Carvera-Community/Carvera_Community_FusionPlugin/issues) and/or in the Makera Discord [#3rd-party-cam](https://discord.com/channels/910194756473225269/1243862379322806284) channel, or in the Community Discord [Fusion add-in](https://discord.com/channels/1341908765212934320/1464378831573090448) channel.
{% endhint %}

The Fusion plugin (add-in) helps you generate GCode files from Fusion 360 by guiding you through selecting compatible setups and then producing g-code files in the structure you prefer. This includes outputing a single large file with multiple operations when using Fusion for personal use. It also includes a few quality-of-life utilities for working with multiple setups on the 4th Axis.

## Download

You can download the [latest version of the Fusion plugin from Github](https://github.com/Carvera-Community/Carvera_Community_FusionPlugin/releases/latest).

## G-code generation options

The plugin provides several g-code options to support indexed 4th Axis workflows:

- **A-axis rotation between setups**: enables indexed milling by having the machine rotate the 4th axis between setups
- **Optional Y-axis retract on rotation**: by default the Z-axis retracts before rotating the A-axis, but if Z retract alone can’t clear the stock, an additional Y-axis move can help reduce the risk of collisions during rotation.
- **Configurable Y retract coordinate (G53/MCS)**: define how far to retract in Y to clear the workpiece. This uses the *G53* (Machine Coordinate System / MCS), so values are absolute and typically negative.
- **Experimental rapid moves**: you can enable higher-speed non-cutting moves. Because it’s not possible to validate every outcome, **verify the generated output before running it live and always observe the machine when using this option**. Feedback is especially valuable while the plugin is in beta.
- **Minimum distance strategy for rapids**: customize the minimum movement distance required before switching to rapid movements.
- **Customizable g-code blocks**: usually no custom g-code is needed, but if desired this option provides flexibility for future changes and special workflows, including:
  - inserting code prior to tool changes
  - detecting the end of an operation
  - detecting the end of the operation header

## Output organization options

Output is designed to be flexible while remaining predictable:

- **Output location and naming**: choose an output folder and an output base name, which is then used to form the final file names depending on grouping options.
- **Numeric-only program names**: force numeric output names for machines that require them.
- **Sequence numbering**: optionally prepend filenames with a sequence number (with a configurable digit count) to preserve operation order in the output folder.
- **Grouping strategy**: choose how output is split:
  - **Single file**: one large program for all setups
  - **Per setup (default)**: one program per setup
  - **Per setup and tool**: split by tool within each setup; if multiple operations use the same tool, they will be combined into one file per tool change
  - **Per operation**: one file per operation
- **Combine operations using the same tool**: reduce file count and tool changes where applicable.
- **Flatten output**: avoid sub-folders by outputting a flat list of files, using setup and operation names as filenames.
- **Overwrite protection**: allow or deny overwriting existing files as a safety measure.
- **Clear output folder before processing**: optionally remove existing files in the output folder to simplify regeneration.

## Other utilities

Beyond output generation, the plugin includes:

- **Translations**: the UI is translatable; currently English and Swedish are available. PRs to add languages or improve translations are welcome.
- **Batch setup renaming**: rename setups in bulk (all setups or only the currently selected ones). If the “search” string is omitted, the behavior changes to prepending setup names with the “replace” string. Python regular expressions are supported for more complex patterns.
- **Per-document settings**: settings are saved per document, and you can save defaults that will be applied to new documents.