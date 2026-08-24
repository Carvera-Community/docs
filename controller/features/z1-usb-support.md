# Z1 USB Support

## Z1 USB Support

The Makera Z1 uses a vendor-class USB interface (`303A:4002`), not a normal serial port.&#x20;

### MacOS

No driver needs to be installed, the connection works straight away when

### Windows

Windows needs the WinUSB driver bound to USB ID `303A:4002`.

1. Download [Zadig](https://zadig.akeo.ie/).
2. Plug in the Z1, then in Zadig choose **Options → List All Devices**.
3. Select the Z1 device (`303A:4002`).
4. Set the driver to **WinUSB** and click **Install Driver** or **Replace Driver**.
5. Replug the cable and connect from the Controller USB list.

### Linux

On Linux, if the Z1 is listed but cannot be opened, the Controller shows an error instead of failing silently. Follow the udev steps below:

Run this command to create the udev rule:

```
sudo sh -c 'echo "SUBSYSTEM=="usb", ATTR{idVendor}=="303a", ATTR{idProduct}=="4002", MODE="0660", GROUP="plugdev", TAG+="uaccess"" > /etc/udev/rules.d/99-makera-z1.rules'
```

After creating the rule, reload udev and replug the cable:

```
sudo udevadm control --reload-rules sudo udevadm trigger
```
