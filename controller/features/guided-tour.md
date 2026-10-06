---
description: The Guided Tour was added in version 2.3.0
---

# Guided Tour

The Controller includes a guided tour that walks new users through the interface. It highlights key UI elements one at a time, with a short explanation of what each one does.

{% embed url="https://www.youtube.com/watch?v=p2mGbvEtsIs" %}

## First run

On the very first launch of the Controller the tour starts automatically with a welcome message. It does not appear for existing installs that have already been configured.

The tour uses a simulated machine and no real connection is needed. A sample toolpath is loaded so the G-code viewer and file-related screens have something to show. If the Controller happens to be connected to a machine when the tour is triggered, a confirmation dialog asks you to disconnect first. The tour will not start over an active job.

## Running the tour again

The tour only runs automatically once. To replay it at any time, open the main menu and select **Help -> Guided Tour**.

<figure><img src="../../.gitbook/assets/Screenshot 2026-10-06 at 1.18.35 pm.png" alt="" width="142"><figcaption></figcaption></figure>

Alternatively You can also force the welcome screen to appear on next launch by setting `tutorial_completed` to `0` in the Controller config file.
