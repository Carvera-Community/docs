# Installation/Upgrade

{% hint style="success" %}
## Makera Support have stated that using the Community Firmware/Controller does not void the machine warranty

Do note that the support they can provide maybe limited, and they may ask you to revert to Makera software to ensure that the issue is not specified to Community code. Reach out via the [bug report button](../controller/features/logging.md#viewing-logs) or in #mods in [Makera Discord](https://discord.gg/xwJMTD22) for Community support.
{% endhint %}

## Installation

{% stepper %}
{% step %}
### Download the latest firmware binary file

The .bin file you want is in assets of [latest release](https://github.com/Carvera-Community/Carvera_Community_Firmware/releases/latest)

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Open Firmware Upgrade Screen

Click the top-right drop down menu <img src="../.gitbook/assets/image (8).png" alt="" data-size="line"> and select the software update option <img src="../.gitbook/assets/image (9).png" alt="" data-size="line">.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
{% endstep %}

{% step %}
### Open Firmware Uploader&#x20;

Click the <img src="../.gitbook/assets/image (5).png" alt="Firmware" data-size="line"> tab and click <img src="../.gitbook/assets/image (6).png" alt="update" data-size="line"> to bring up the file upload interface

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>


{% endstep %}

{% step %}
### Upload new firmware file

Select the .bin firmware binary you downloaded in step #1 and click <img src="../.gitbook/assets/image (4).png" alt="Upload" data-size="line"> and wait for the uploading to finish, the machine will be reset automatically by default. Or you can manually reset the machine using the prompt.
{% endstep %}

{% step %}
### Check firmware version

After resetting, you will need to reconnect the Controller. You can check if the firmware version has been updated by reopening the upgrade window, or manually running the 'version' command in the MDI window.

<figure><img src="../.gitbook/assets/image (10).png" alt="" width="360"><figcaption></figcaption></figure>
{% endstep %}
{% endstepper %}

