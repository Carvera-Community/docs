# Supported OS

The Controller software works on the following systems:

* Windows 7 x64 or newer
* MacOS using Intel CPUs running Ventura (13) or above
* MacOS using Apple Silicon CPUs running Sonoma (14) or above
* Linux using x64 CPUs running a Linux distribution with Glibc 2.35 or above (eg. Ubuntu 22.04 or higher)
* Linux using aarch64 CPUs (eg Raspberyy Pi 3+) running a Linux distribution with Glibc 2.39 or above (eg. Ubuntu 24.04 or higher)
* Apple iPad with iOS 17.6 or higher
* Android devices with Android 11 or higher running ARM 32 and 64-bit processors (ARMv7a and ARMv8a) and x86\_64
* Other systems might be work via the Python Package, see [Python Package](where-to-get.md#python-package) for more details.

## OS Specific Notes

### MacOS

You may get the error "Apple could not verify “Carvera Controller Community” is free of malware that may harm your Mac or compromise your privacy." as we do not currently sign our MacOS releases.

You can overcome this issue by opening System Settings, then click Privacy & Security in the sidebar.  Scroll to the bottom and click "Open Anyway". After doing this once the App can be opened normally.

<figure><img src="../.gitbook/assets/Screenshot 2026-01-10 at 2.05.06 pm.png" alt=""><figcaption></figcaption></figure>

### Android

When using the file browser in the Controller, the app will guide you to a permission page of android where you have to grant the app full access to your android devices files. Without this you will not see any files.

Be aware that there is a known bug in one of the libraries used for graphics rendering, this can result in the screen stay black after starting the app. Until this is resolved in the upstream library we have implemented a workaround to try to prevent this from occurring. If you still encounter this issue, you then need to go to the home screen and back to the app. Please give feedback via [github issue](https://github.com/Carvera-Community/Carvera_Controller/issues/new) if this occurs for you and we can work together to improve our workaround for your device.

### Linux

For Linux support we build an AppImage, these are a self-contained binary with all the required dependencies to run the application.

To use it, first make it executable (`chmod +x carveracontroller-community-<version>-<arch>.appimage`).

Then you will be able to run it.

If you want a shortcut, consider using [AppImageLauncher](https://github.com/TheAssassin/AppImageLauncher).

#### Arch Linux

For the Carvera controller to connect to the machine over USB on ArchLinux, a udev rule must be created granting the user permissions to the USB device when it is connected.

1. Add a new udev file:

```
sudo vim /etc/udev/rules.d/99-carverausb.rules
```

2. Add the following contents:

```
# Carvera USB Serial Device
SUBSYSTEM=="tty", ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001", MODE="0666"

# Optional Jog Pendant USB device
SUBSYSTEM=="tty", ATTRS{idVendor}=="10ce", ATTRS{idProduct}=="eb93", MODE="0666"
```

3. After saving and closing the file, reload the rules:

```
sudo udevadm control --reload-rules
sudo udevadm trigger
```

### iOS

The iOS build of the Carvera Community Controller may lag behind other releases due to Apple App Store review and developer availability.
