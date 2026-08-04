---
description: Communication Protocol switching was added in version 2.2.0c
---

# Communication Protocol

Community firmware can speak either the Smoothieware-style line protocol or Makera’s framed protocol. Makera Studio and newer Makera Controller expects this Makera protocol.

The default protocol type is `makera`

Switching to `smoothie` restores classic Smoothieware line I/O (Community Controller default behaviour historically).

## Switch at runtime

| Command | Effect |
| ------- | ------ |
| [M485](#m485-report-protocol) | Report current protocol |
| [M485.1](#m485.1-smoothie-protocol) | Switch to Smoothie protocol |
| [M485.2](#m485.2-makera-protocol) | Switch to Makera protocol |

Runtime changes are not persisted. Use [`config-set`](../supported-commands/console-commands/README.md) to change the boot default:

Runtime changes are not persisted, use `config-set sd protocol <mode>` to change the boot default.
