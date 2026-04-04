# Spindle maximum RPM

{% include "../../.gitbook/includes/dev-feature-warning-banner.md" %}

Community firmware enforces a **maximum spindle speed** so commanded RPM (for example from **M3** / **S**) is **clamped** to a safe upper limit for your machine and spindle.

## Configuration

The limit is stored as **`spindle.max_rpm`** (writable with `config-set` like other settings). Typical defaults are **15000** on **Carvera (C1)** and **13000** on **Carvera Air**.

Example:

```
config-get sd spindle.max_rpm
config-set sd spindle.max_rpm 13000
```

After modifying the setting on the sd card, apply with a **`reset`** or reboot.

## Behaviour

If a program requests **S** above **`spindle.max_rpm`**, firmware limits the **target RPM** to the configured maximum (see spindle module implementation). Set the cap to match your **actual spindle rating** and any **collet or tooling** limits.
