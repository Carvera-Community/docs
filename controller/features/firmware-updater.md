---
description: The Firmware Update Screen was reworked in version 2.3.0
---

# Firmware Updater

The Controller includes a built-in update screen for upgrading both the Controller application and the machine firmware. Open it from the top-right menu dropdown.

## Checking for Updates

Version data is fetched directly from the Carvera-Community GitHub Releases. The screen shows the latest available version for both the Controller and Firmware side by side, with a clear indication of whether:

* An **update is available**
* You are **already up to date**
* You are **running ahead** of the latest release (e.g. a development build)

A **Stable / RC channel toggle** lets you switch between Stable releases and Release Candidates without leaving the screen.

## Inline Release Notes

Full changelogs from GitHub are parsed and displayed with category badges (**Enhancement**, **Fixed**, **Changed**) and clickable links, so you can see what changed before updating.

## Updating the Controller

The Controller tab shows a download button that links to the correct installer for your OS and architecture:

* Windows (x64)
* macOS (Intel / Apple Silicon)
* Linux (x64 / ARM)
* Android

On iOS, Controller updates are delivered through the App Store.

## Updating Firmware

### One-click install

On supported machines (C1, CA1, and Z1), the Firmware tab shows an **Install Firmware** button. This:

1. Downloads the firmware binary from GitHub over HTTPS.
2. Verifies the file's **SHA-256 checksum** and size against the values published in the release.
3. Uploads the verified binary to the machine.
4. Prompts you to reset the machine to apply the update.

A confirmation dialog shows exactly where the file will be placed and reminds you to back up your configuration first. Progress is shown during both the download and upload steps, and either can be cancelled.

If the release does not include a checksum, or the connected machine model is not supported for one-click install, the button is disabled with an explanation.

### Install from file

The **Install from file…** button is always available as a fallback. It opens the file browser so you can select a `.bin` file from your computer. This is the same upload workflow described in [Installation/Upgrade](../../firmware/installation-upgrade.md).

### Z1 firmware type detection

The updater auto-detects the type of firmware file selected (whether via one-click or install-from-file):

| Firmware type | Install method |
| --- | --- |
| **Combined LPC+ESP bundle** | Uploaded to the SD card as `firmware.bin` |
| **ESP-only image** | Sent via WiFi OTA to the machine's HTTP updater |
| **LPC-only image** | Uploaded to the SD card as `lpc1768.bin` |

C1 and Air firmware is always installed as `firmware.bin`.
