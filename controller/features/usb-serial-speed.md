# USB serial speed

When the machine is running **Community firmware** that supports it (2.1.0 and above), the Controller can negotiate with the machine to use a **higher USB serial baud rate** for higher throughput.

Enable the option and set the **baud rate** in **Settings** under the Controller options. On connect, the Controller will send the firmware **`baud <rate>`** command and reopens its USB port at the same speed so both sides stay in sync.

<figure><img src="../../.gitbook/assets/Screenshot 2026-04-05 at 10.03.27 am.png" alt="" width="375"><figcaption></figcaption></figure>

If the machine does not support the feature, communication stays at the usual **115200** default.

You can confirm the current serial speed via the `baud` command

Firmware behaviour is documented in [USB serial baud rate](../../firmware/features/usb-serial-baud-rate.md).
