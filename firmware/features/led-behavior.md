# LED Behaviour

The Community firmware drives the **RGB LEDs** on the **Carvera (C1)** and **Carvera Air**. Colours and patterns reflect **machine state** (idle, running, homing, held, tool change, and so on).

***

## Carvera (C1)

### Steady colours

| State     | Colour (typical)     |
| --------- | -------------------- |
| **IDLE**  | Blue                 |
| **RUN**   | Green                |
| **HOME**  | Yellow (red + green) |
| **ALARM** | Red                  |
| **SLEEP** | White (all channels) |

### Blinking patterns

* **HOLD** — green blinks (feed hold).
* **SUSPEND** — blue blinks.
* **WAIT** — yellow blinks (red + green).
* **TOOL** (manual tool change / collet prompt) — two styles:
  * **Collet change** expected (`target_collet_type == 0`): **cyan** (green + blue) blink.
  * **Manual Tool Change only** change: **yellow** blink (red + green).

### Long press behaviour

While the button is held beyond **`main_button_long_press_time`** (default **3000** ms), the **red** channel toggles on the C1 LED as a visible “long press triggered” cue. What the long press **does** when released depends on firmware configuration and state (halt, resume, tool prompts, etc.); the LED only shows that the hold threshold is exceeded.

***

## Carvera Air

The Air uses a **addressable led strip** updated from a periodic **LED tick** and from **button** logic.

### Steady colours

When the machine **enters** a new state, the ring is set to:

| State     | Pattern |
| --------- | ------- |
| **IDLE**  | Blue    |
| **RUN**   | Green   |
| **HOME**  | Orange  |
| **ALARM** | Red     |
| **SLEEP** | White   |

### TOOL state — slot hints on the ring

In **TOOL**, when the planner is idle, the ring can indicate the **target tool slot** (for slots **1–6**) by lighting **segments** (count or pattern). Colours match the C1 logic: **cyan** when a **collet change** is expected, **yellow** when it is a **tool-only** change. For other slot numbers, the firmware uses a **full-colour blink** instead of a segment count.

### RUN — optional red flash (`check_led`)

If the internal **check LED** flag is on (see below), during **RUN** the ring briefly shows **red** on some ticks. That is intended as an extra **attention** signal (for example factory or diagnostic use), not as the normal running indication.

***

## Long-press progress on the Air

If **`main_button_long_press_enable`** is set to a non-empty string, a **long press** (before the hold threshold is reached) can show **progress** on the led strip as **filled segments** (roughly 0–20–40–60–80–100% of **`main_button_long_press_time`**).
