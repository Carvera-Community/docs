---
description: Workspace Management was added in version 0.10.0
---

# Workspace Management

As you know the machine uses different Coordinate systems, commonly referenced as Work Coordinate System (WCS) and Machine Coordinate System (MCS). But did you know its possible to have multiple Work Coordinate Systems?&#x20;

The default WCS is called `G54`, but others are available via G55-G59.3. When using Carvera Community Firmware 1.0.9c+ together with v0.10.0+ of the Community Controller you can now easily change between the different WCS systems via the Top Bar, and advanced WCS management screens. Each WCS will store it's own offsets to EEPROM.&#x20;

Multiple WCS are useful for:

* Running different setups or fixtures: You can quickly switch between different parts or jigs without having to re-probe or redefine zero locations.
* Repeating jobs in multiple locations: If you have several identical parts on the same machine bed, you can assign each one a different WCS (e.g., G54 for part 1, G55 for part 2), speeding up the workflow and reducing setup errors.
* Managing multi-operation projects: For complex jobs requiring multiple machining operations or tool changes, you can assign each operation its own WCS, making it easier to maintain consistency.
* Training and testing: Multiple users can each have their own WCS for testing and practice without interfering with each other’s offsets.

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption><p>Workspace Top Bar Dropdown</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/workspace_settings.png" alt=""><figcaption><p>Advanced WCS Settings Screen</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Selected Workspace is displayed in Config and Run screen</p></figcaption></figure>
