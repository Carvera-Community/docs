# MDI Terminal

The **MDI** (Manual Data Input) area is where you send individual G-code lines or short programs to the machine without loading a full file.\
\
To access the MDI, click the button that says MDI in the bottom left corner of the first control screen. It will swap to saying File and show a terminal instead of the file contents

<figure><img src="../../.gitbook/assets/Screenshot 2026-04-08 at 10.52.08 pm.png" alt="" width="375"><figcaption><p>File View with arrow highlight MDI button</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/Screenshot 2026-04-08 at 10.53.40 pm.png" alt="" width="375"><figcaption><p>MDI Terminal open</p></figcaption></figure>

## Sending commands

* **Ctrl+Enter** sends the contents of the MDI box to the machine.
* **Enter** alone adds a **new line** in the input (you can compose **multi-line** snippets before sending).
* You can send **several commands at once**; output shows **multi-line** responses in a readable way.

## History

* Press the **up arrow** in the MDI field to recall the **last sent** command.
* You can step through **multiple** previous commands with the **up** and **down** arrow keys.
* Double click a previous command in the terminal history to copy it to the current MDI input box

## Keyboard shortcuts

* **Ctrl+,** — open **Settings**.
* **Ctrl+M** — focus / jump to **MDI** quickly.

## Focus and jogging

When the **MDI text box has focus**, **keyboard jogging** is disabled so typed keys do not move the machine. Click outside the field or use the UI to jog if needed.

## MDI while the program is running

Whether you can send MDI during playback depends on Controller setting **allow MDI while running**.

This setting is for advanced users and can lead to some machine problems if the wrong code is sent at the wrong time.
