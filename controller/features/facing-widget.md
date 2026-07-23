---
description: Facing Wizard was added in version 2.2.0
---

# Facing Wizard

The wizard takes a number of inputs and generates a facing toolpath for you without you needing to open a CAM.

If the Z-grid probing option is used, the wizard will find the highest point on the stock and use that as the starting point.

You can open the Facing wizard from the Tools section of the main control page of the Controller UI.

<figure><img src="../../.gitbook/assets/Screenshot 2026-07-23 at 4.12.17 pm.png" alt=""><figcaption></figcaption></figure>

## What it does

* Collects stock size, tool, stepover, depth, milling direction, and related parameters
* Optionally probes a Z grid over the area before facing
* Previews the toolpath envelope and G-code
* Writes a temporary `.nc` you can upload/run like any other file
* Supports load / save / delete presets

Selected probe tool and collet choices are kept when you reopen the wizard.

## Screenshots

<div><figure><img src="../../.gitbook/assets/589978347-2d3c1200-a11a-4758-be83-5e32d5aed98e.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/589978450-57831e9c-f6fa-418e-8886-61c1849be53a.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/590110603-5f5254e4-e28c-4e31-981d-05fb82ddd23a.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/590110647-befd9259-b1d0-44be-9916-470f290c21b8.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/590110677-69c3974b-cd54-4f89-83c8-2c0c4c8465c2.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/590110700-599b1513-a935-4ad5-ad73-056d1b5e882f.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/590110731-aba1eaa0-51b0-45d9-92de-4b7a508b4923.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/590110768-c0e29a01-a4c1-4fec-8669-f2fde9c0cdcf.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/590110787-2de1f935-27ae-440e-b27e-859230dba320.png" alt=""><figcaption></figcaption></figure> <figure><img src="../../.gitbook/assets/590110819-952c28b9-c2f9-4877-b007-7594f78a613a.png" alt=""><figcaption></figcaption></figure></div>
