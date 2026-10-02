---
description: Z1 Camera support was added in version 2.2.0; Timelapse in 2.3.0
---

# Z1 Camera

On a Makera Z1 connected over WiFi, the Controller supports viewing the built-in camera. When found, a camera button appears in the G-code viewer toolbar.

<figure><img src="../../.gitbook/assets/Screenshot 2026-10-02 at 10.06.39 pm.png" alt=""><figcaption></figcaption></figure>

Tap it to start or stop the live stream. If the stream drops, the viewer automatically reconnects and shows a spinner until the feed resumes. While streaming, the configure panel offers:

* **Resolution** — changeable live (640×480 default; also 800×600, 1024×768, 1280×720, 1280×1024, 1600×1200). Higher sizes may run at a lower frame rate depending on the quality of the wifi connection.
* **Brightness**, **Contrast**, **Gamma** adjustment

<figure><img src="../../.gitbook/assets/Screenshot 2026-10-02 at 10.07.30 pm.png" alt="" width="285"><figcaption></figcaption></figure>



## Timelapse

On the Z1, the Controller can trigger the machine's built-in timelapse recording. Enable **Record Timelapse** on the Config and Run screen before starting a job. While the machine is recording, a red recording indicator appears on the camera button.

<figure><img src="../../.gitbook/assets/Screenshot 2026-10-02 at 10.08.24 pm.png" alt="" width="563"><figcaption></figcaption></figure>

The timelapse status (recording state, file transfer activity, and SD card space) is shown in the camera settings panel while it is open.

Recorded videos are stored on the machine's SD card under `/sd/videos`. When that folder exists, the [File Browser](file-browser.md) can open it for downloading or deleting recordings.

{% hint style="warning" %}
Timelapse is an feature of the Makera esp32 firmware.The follow are some known issues:

1. Sometimes it doesn't stop recording when gcode file playback has finished. The only way the only fix seems to be to just power cycle the machine using the switch at the back.
2. Video files that are currently being written are visible in the file browser but cannot be downloaded. A generic download error is returned until the ESP releases it's file handle on the file
3. MD5 hashes returned by the machine for the video files are incorrect. For some reason the ESP calculates wrong hashes. MD5 related validation errors are suppressed in the Controller specifically for video files.
4. File transfer speeds are slow in general on the Z1. This is quite noticeable when you start trying to transfer the video files. It's quicker to eject the SD card and connect it directly to a computer to transfer.
{% endhint %}
