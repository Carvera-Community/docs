# baud

Query or change the **USB serial** baud rate on the USB serial interface.

The rate set with **`baud <rate>`** is **temporary** intentionally to not leave the machine in a potentially broken and unreachable state. After **15 seconds** with **no** incoming serial activity, firmware restores the **default** baud of 113200.

### Usage

**Query current rate** :

```
baud
```

**Set rate** (must be a positive integer, maximum **4000000**):

```
baud <rate>
```

Example:

```
baud 1500000
```

On success the firmware replies with `ok` and switches the UART immediately. Your **host** must reopen or reconfigure its serial port to the **same** rate or communication will be garbled.

### Errors

* `error:Serial console not available` — no primary serial console (unusual on normal builds).
* `error:Invalid baud rate` — missing/invalid number, zero, negative, or above **4000000**.
