---
description: Docker Container support was added in version 0.10.0
---

# Controller in a Web Browser

For users comfortable running Linux Containers the controller can be under Docker, which is then access via a browser or VNC client. This enables you to run the controller on a remote machine and access it from a web browser from multiple locations, and thus overcome the single-network-connection at a time limitation.

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption><p>Carvera Controller in a Web Browser</p></figcaption></figure>

The docker image expects a volume `/config` which is used to store the configuration and log files. If not provided, the application will run, but will not persist any configuration or log files.

The docker image is available on [GitHub Container Registry](https://ghcr.io/carvera-community/carvera-controller) with the following tag patterns:

* latest - The latest tagged release version
* dev - The latest development build
* x.y.z - A specific tagged version

The latest reeleased version can be pulled with the following command:

```
docker pull ghcr.io/carvera-community/carvera-controller-<arch>:latest
```

Where `<arch>` is `x64` or `arm64` depending on your system architecture. To run the docker image, use the following command:

```
docker run -p 5900:5900 -p 8080:8080 -v /path/to/config:/config ghcr.io/carvera-community/carvera-controller-<arch>:latest
```

The application can then be accessed via a web browser at `http://<host>:8080` or via a VNC client at `<host>:5900`. The VNC connection does not require a password.
