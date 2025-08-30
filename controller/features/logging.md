---
description: Logging support was added in version 2.0.0-RC1
---

# Logging

The Controller can write logs to file with configurable levels of detail. The commands sent/recieved by the MDI are included in the **INFO** level of logging.

## Configuration

The logging settings are found in **Settings** <img src="../../.gitbook/assets/image (18).png" alt="" data-size="line">, in the **Controller** section:

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

## Viewing Logs

After enabling logging each time the application is opened a new log file will be created in the users home directory `~/.kivy/logs/` with the name pattern kivy\_YY-MM-DD\_NN.txt

This path will be opened if clicking the bug report button in the UI:&#x20;

<figure><img src="../../.gitbook/assets/image (21).png" alt="" width="557"><figcaption></figcaption></figure>



&#x20;
