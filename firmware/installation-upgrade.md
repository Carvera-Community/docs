# Installation/Upgrade

{% hint style="success" %}
#### Makera Support have stated that using the Community Firmware/Controller does not void the machine warranty

Do note that the support they can provide maybe limited, and they may ask you to revert to Makera software to ensure that the issue is not specified to Community code. Reach out via the [bug report button](../controller/features/logging.md#viewing-logs) or in #mods in [Makera Discord](https://discord.gg/xwJMTD22) for Community support.
{% endhint %}

## Installation

{% stepper %}
{% step %}
**Download the latest firmware binary file**

The .bin file you want is in assets of [latest dev release](https://github.com/Carvera-Community/Carvera_Community_Firmware/releases/tag/dev)

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
**Open Firmware Upgrade Screen**

Click the top-right drop down menu <img src="../.gitbook/assets/image (8).png" alt="" data-size="line"> and select the software update option <img src="../.gitbook/assets/image (9).png" alt="" data-size="line">.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
**Open Firmware Uploader**

Click the <img src="../.gitbook/assets/image (5).png" alt="Firmware" data-size="line"> tab and click <img src="../.gitbook/assets/image (6).png" alt="update" data-size="line"> to bring up the file upload interface

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
**Upload new firmware file**

{% hint style="info" %}
If you are using Makera's Controller software it can only select firmware binary files if the file is called "firmware.bin". Rename the file if you are using Makera's Controller software. The Community Controller will allow you to select any .bin file.
{% endhint %}

Select the .bin firmware binary you downloaded in step #1 and click <img src="../.gitbook/assets/image (4).png" alt="Upload" data-size="line"> and wait for the uploading to finish, the machine will be reset automatically by default. Or you can manually reset the machine using the prompt.
{% endstep %}

{% step %}
**Check firmware version**

After resetting, you will need to reconnect the Controller. You can check if the firmware version has been updated by reopening the upgrade window, or manually running the 'version' command in the MDI window.

<figure><img src="../.gitbook/assets/image (10).png" alt="" width="360"><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

## Alternative Install Method

If it's not possible to transfer the firmware using the Controller software it is always possible to change the firmware (even back to the Makera firmware) by:

1. Removing the SD card from the machine control board
2. Insert the SD card to a computer
3. Delete the `FIRMWARE.CUR` file
4. Copy the new firmware file to the root of the card with the filename `firmware.bin`
5. Next time the control board powers on, it will flash this firmware file to itself
