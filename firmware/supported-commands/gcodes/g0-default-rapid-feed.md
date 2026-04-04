# G0 — Rapid positioning

## G0 — Rapid move

### Description

**G0** performs a rapid, non-cutting move to the programmed position. On Community firmware, the feed rate for **G0** is handled differently from **G1**:

* **F** on a **G0** line applies **only to that line**. It does **not** update the modal feed used by later **G1** / **G2** / **G3** moves.
* If **G0** is issued **without F**, the move uses the **default seek rate** from configuration (`default_seek_rate`, mm/min), **not** the last **G1** **F** value. This defaults to **3000** mm/min.

### Parameters

* **X**, **Y**, **Z**, **A**, …: target position in the active coordinate system (same as standard G0).
* **F**: optional feed rate for **this G0 line only** 

### Configuration

* **`default_seek_rate`** — rapid speed used for **G0** when **F** is omitted. Set with `config-set` like other machine settings, for example:

```
config-get sd default_seek_rate
config-set sd default_seek_rate 4000
```

### Example

```gcode
G21 G94
G1 F600 Z5
G0 X50 Y30          ; rapid at default_seek_rate, not 600 mm/min
G0 X0 Y0 F12000     ; this line only uses 12000 mm/min
G1 Z-1 F300         ; feed is 300 mm/min; the G0 F did not carry over
```

### See also

* [Smoothieware G0 reference](https://smoothieware.org/g0)
