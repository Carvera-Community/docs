# Inverse time feed (G93) and feed per minute (G94)

{% include "../../../.gitbook/includes/dev-feature-warning-banner.md" %}

Community firmware supports **G93** (inverse time feed) and **G94** (feed per minute), similar in spirit to [LinuxCNC G93 / G94](http://linuxcnc.org/docs/html/gcode/g-code.html#gcode:g93-g94). They are **modal**: once set, the mode stays in effect until the other command is programmed or the program ends with **M2** / **M30**.

---

## G93 — Inverse time feed mode

### Description

**G93** selects **inverse time feed**. On each **G1**, **G2**, or **G3** move, the **F** word is **not** a speed in mm/min. Instead the planner converts it using the **length of that move** so the move executes in a well-defined time.

This mode is intended for **multi-axis moves** (for example simultaneous linear and **A**-axis motion) where a single **F** in mm/min would not describe the motion as clearly as “complete this block in a given time.”

### How F is interpreted

The firmware treats **F** as having units of **1/minute** (reciprocal minutes) for the block:

* **Time to complete the move** ≈ **1 / F** (in minutes), when **F** is positive.
* The planner turns that into an effective **mm/min** for the path by multiplying **F** by the **move length** used internally (same net effect as scaling feed by distance for that block).

So **larger F** means **shorter** block time (faster), **smaller F** means **longer** block time (slower). **F** must be **positive**.

### Rules for G1, G2, and G3

* **Every** **G1**, **G2**, and **G3** line must include a valid **F** while **G93** is active. If **F** is missing, the machine **halts** with an error such as: `Inverse-time feed mode requires F parameter on every G01/G02/G03 line.`
* **G0** (rapid) does **not** use inverse time: the firmware runs rapids at **mm/min** using the normal [rapid / seek behavior](g0-default-rapid-feed.md) (**default_seek_rate** or **F** on that **G0** line only). The **G93** modal state remains on for subsequent **G1**/**G2**/**G3** moves.

### Arcs (G2 / G3)

Arcs are broken into segments. In **G93**, the **total** time implied by **F** for the arc is **split across segments** in firmware so the whole arc matches the programmed inverse-time feed.

### Rotary (A-axis) moves

For **A**-only or auxiliary moves where distance is in **degrees**, the same inverse-time scaling uses that distance in the planner. Combined **XYZ + A** moves use the full path length as computed by the firmware (including rotary compensation where applicable). If something looks off for pure rotary blocks, verify **F** on **every** line and compare with **G94** + mm/min for the same path.

### Parameters

* **G93** on its own line has **no** parameters.

### Example

```gcode
G21
G94
G1 X0 Y0 F2000        ; normal: 2000 mm/min

G93                   ; inverse time on
G1 X10 Y0 F4          ; F applies to this block only; planner derives mm/min from move length
G1 X20 Y0 F8          ; each G1 must carry F while G93 is active

G94                   ; back to mm/min
G1 X30 F1500
```

---

## G94 — Feed per minute mode

### Description

**G94** selects **feed per minute** mode (the usual behaviour on the Carvera). The **F** word on **G1**, **G2**, and **G3** is the feed rate in **mm/min** (with **G21**). **G0** continues to use seek rate rules as documented on the [G0 rapid feed](g0-default-rapid-feed.md) page.

**M2** and **M30** also clear inverse time and restore the default expectation of **G94**-style handling for feed.

### Parameters

* **G94** on its own line has **no** parameters.

### Example

```gcode
G21 G94
G1 X10 Y10 F1200      ; 1200 mm/min along the move
```
