---
description: Most MDI Terminal enhancements were added in version 2.1.0
---

# MDI Terminal

The **MDI** (Manual Data Input) area is where you send individual G-code lines or short programs to the machine without loading a full file.\
\
To access the MDI, click the button that says MDI in the bottom left corner of the first control screen. It will swap to saying File and show a terminal instead of the file contents

<figure><img src="../../.gitbook/assets/Screenshot 2026-10-02 at 9.25.15 pm.png" alt="" width="563"><figcaption><p>File View with arrow highlight MDI button</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2026-10-02 at 9.27.57 pm.png" alt="" width="563"><figcaption><p>MDI Terminal open</p></figcaption></figure>

## Sending commands

* **Ctrl+Enter** sends the contents of the MDI box to the machine.
* **Enter** alone adds a **new line** in the input (you can compose **multi-line** snippets before sending).
* You can send **several commands at once**; output shows **multi-line** responses in a readable way.

## History

* Press the **up arrow** in the MDI field to recall the **last sent** command.
* You can step through **multiple** previous commands with the **up** and **down** arrow keys.
* Double click a previous command in the terminal history to copy it to the current MDI input box

## Keyboard shortcuts

Keyboard short cuts can be [remapped](keyboard-shortcuts.md), but the defaults are:

* **Ctrl+,** — open **Settings**.
* **Ctrl+M** — focus / jump to **MDI** quickly.

## Focus and jogging

When the **MDI text box has focus**, **keyboard jogging** is disabled so typed keys do not move the machine. Click outside the field or use the UI to jog if needed.

## Intellisense

While typing in the MDI input box, an **Intellisense-like popup** appears showing the command name, a short description, and parameter details for recognised G-codes, M-codes, and console commands. The same popups appear when selecting a line in the G-code file viewer.

<figure><img src="../../.gitbook/assets/Screenshot 2026-10-02 at 9.30.49 pm.png" alt="" width="375"><figcaption></figcaption></figure>



The syntax highlighter also colours G/M codes, comments, O-code constructs, and SimpleShell commands in the MDI history.

## Auto-correct command case

When enabled (the default), commands typed in lowercase are automatically corrected to their canonical case before being sent. For example, `g0 x10 f500` is sent as `G0 X10 F500`. The correction applies to G-codes, M-codes, and known parameter letters. Comments are left untouched.

This can be toggled in **Settings -> Auto-Correct MDI Command Case**.

## MDI while the program is running

Whether you can send MDI during playback depends on Controller setting **allow MDI while running**.

This setting is for advanced users and can lead to some machine problems if the wrong code is sent at the wrong time.
