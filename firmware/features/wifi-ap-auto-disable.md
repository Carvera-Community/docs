---
description: WiFi AP Auto-Disable was added in version 2.2.0c
---

# WiFi AP Auto-Disable

When the machine joins an external WiFi network (STA), the on-board access point will turned off automatically so the hotspot does not stay active needlessly.

This feature is enabled by default (`wifi.ap_auto_disable true`).

To keep the AP running even while STA is connected:

```
config-set sd wifi.ap_auto_disable false
```

Restart after changing. Manual [`ap disable`](../supported-commands/console-commands/README.md) / [`ap enable`](../supported-commands/console-commands/README.md) still work as before. 
