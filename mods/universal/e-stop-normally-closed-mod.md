---
description: Guide originally contributed by Discord user F355
---

# Normally-Closed E-stop

The stock e-stop button shipped with Carvera and Carvera Air is wired as normally-open (NO). This means the machine will run with no button attached at all, and pressing a faulty button that fails to close the contact has no effect — a serious safety hazard.

This mod rewires the button to normally-closed (NC) and updates the firmware pin polarity to match, so the machine halts if the button circuit is broken for any reason.

**What you need:** a small Phillips screwdriver.

**Steps:**

1. Remove the 4 screws from the top of the e-stop button enclosure and open it.
2. Unplug the red wire from the **NO** terminal and move it to the **NC** terminal.
3. Reassemble the enclosure.
4. Start the machine **without** the e-stop button plugged in.
5. In the controller MDI console, run:\
   `config-set sd e_stop_pin 0.20!^`
6. Plug in the e-stop button and restart the machine.

The machine will now stop if the e-stop circuit is open (button pressed, button unplugged, or wire fault).
