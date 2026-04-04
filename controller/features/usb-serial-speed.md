# Higher USB serial speed

When the machine is running **Community firmware** that supports it (2.1.0 and above), the Controller can negotiate with the machine to use a **higher USB serial baud rate** to reduce traffic bottlenecks.

Enable the option and set the **baud rate** in **Settings** under the Controller options that apply to USB serial. On connect, the Controller sends the firmware **`baud <rate>`** command and reopens its USB port at the same speed so both sides stay in sync.

If the machine does not support the feature, communication stays at the usual **115200** default.

Firmware behaviour (idle timeout, persisting **`uart.baud_rate`**, and console usage) is documented in [USB serial baud rate](../../firmware/features/usb-serial-baud-rate.md).
