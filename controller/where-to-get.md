# Where to Get

## Latest Release Version

See the assets section of [latest release](https://github.com/carvera-community/carvera_controller/releases/latest) for installation packages for your system.

* carveracontroller-community-\<version>-windows-x64.exe - Standalone Windows binary, without a installer
* carveracontroller-community-\<version>-Intel.dmg - MacOS with Intel CPU
* carveracontroller-community-\<version>-AppleSilicon.dmg - MacOS with Apple CPU (M1 etc)
* carveracontroller-community-\<version>-x86\_64.appimage - Linux AppImage for x64 systems
* carveracontroller-community-\<version>-arm664.appimage - Linux AppImage for aarch64/arm64 systems
* carveracontroller-community-\<version>.apk - Android installable package
* carvera\_controller\_community-\<version>-py3-none-any.whl - Python wheel package

## Latest Development Version

Dev builds of Carvera Controller Community are automatically compiled after every new commit to the `develop` branch. This means that each build incorporates the most recent changes and improvements. While these builds offer a glimpse into the ongoing development of Carvera Controller, keep in mind that they are still works in progress and may contain bugs or unstable features. The latest dev build files can always be accessed [here](https://github.com/Carvera-Community/Carvera_Controller/releases/tag/dev). The release notes section on that page shows what new functionality has been added.

## Python Package

It's best to use one of the pre-built packages as they they have frozen versions of tested dependencies and python interpreter, however if you prefer the software can be installed as a Python package. This might allow you to use a unsupported platform (eg raspi 1) provided that the dependencies can be met.

```
pip install carvera-controller-community
```

Once installed it can be run via the module

```
python3 -m carveracontroller
```

## Linux Container

The container image is available on [GitHub Container Registry](https://ghcr.io/carvera-community/carvera-controller) with the following tag patterns:

* latest - The latest tagged release version
* dev - The latest development build
* x.y.z - A specific tagged version

The latest released version can be pulled with the following command:

```
docker pull ghcr.io/carvera-community/carvera-controller-<arch>:latest
```

Where `<arch>` is `x64` or `arm64` depending on your system architecture. To run the docker image, use the following command:

```
docker run -p 5900:5900 -p 8080:8080 -v /path/to/config:/config ghcr.io/carvera-community/carvera-controller-<arch>:latest
```

The application can then be accessed via a web browser at `http://<host>:8080` or via a VNC client at `<host>:5900`. The VNC connection does not require a password. See [Controller in Web Browser](features/controller-in-a-web-browser.md) for more details on this functionality.

## iOS

The iOS build of the Carvera Community Controller is available on  the [Apple App store](https://apps.apple.com/us/app/carvera-community-controller/id6743028299).
