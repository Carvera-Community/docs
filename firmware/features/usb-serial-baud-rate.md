# USB serial baud rate

{% include "../../.gitbook/includes/dev-feature-warning-banner.md" %}

Community firmware lets you run the **main USB serial console** faster than default when the host supports it. Higher rates improve transfer speeds when streaming large gcode programs.

## Default

At boot the USB Serial speed is by default **115200** bps.

## Runtime: `baud` console command

You can change the active speed **immediately** with the [**`baud`**](../supported-commands/console-commands/baud.md) console command:

```
baud 1500000
```

The host must switch to the **same** baud on its side at once, or bytes will be unreadable.

### Temporary change and idle timeout

A speed set via **`baud <rate>`** is tracked as **temporary** inside the serial driver. If there is **no serial receive activity for about 15 seconds**, firmware **reverts** the UART back to 115200.

## Limits

The console command accepts rates from **1** to **4000000** bps (see firmware validation). Not every value is practical for every host OS or cable; if the link fails, it falls back to **115200**.
