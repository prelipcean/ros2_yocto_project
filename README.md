# ros2_yocto_project

This repository provides a Docker-based development environment for building and integrating ROS2 with the Yocto Project for embedded Linux systems.

---

## Project Overview

- **Goal:** Integrate ROS2 into custom embedded Linux images using the Yocto Project.
- **Tools:** Docker, Yocto Project (Scarthgap 5.0), ROS2

---

## References

- **ROS2 Documentation:** [ROS2 Jazzy](https://docs.ros.org/en/jazzy/)
- **Yocto Project Release:** [Scarthgap 5.0 (LTS)](https://www.yoctoproject.org/development/releases/)
  - Released: April 2024
  - Latest: 5.0.10 (June 2025)
  - LTS until April 2028
- **Yocto Documentation:** [Yocto Project 5.0.10 Docs](https://docs.yoctoproject.org/5.0.10/)

---

## Getting Started

### 1. Build the Docker Image

```sh
docker build -t yocto-builder -f docker/Dockerfile.yocto .
```

### 2. Prepare Your Workspace

```sh
mkdir ~/yocto-workspace
```

### 3. (Optional) Open Firewall Port

```sh
sudo ufw allow 8080/tcp
sudo ufw reload
```

### 4. Run the Container

By default, the VS Code Server may ignore the `--bind-addr` option and run on port 8080.  
Use the following command to map port 8080:

```sh
docker run --rm -it -p 8080:8080 -v ~/yocto-workspace:/home/devuser/workspace yocto-builder:latest
```

- The VS Code Server will be available at [http://localhost:8080](http://localhost:8080).

You can also map persistent download and sstate-cache directories:

```sh
docker run --rm -it \
  -p 8080:8080 \
  -v ~/yocto-workspace:/home/devuser/workspace \
  -v ~/yocto-downloads:/home/devuser/workspace/downloads \
  -v ~/yocto-sstate:/home/devuser/workspace/sstate-cache \
  yocto-builder
```

> **Note:** By running the VS Code Server, you agree to the [Visual Studio Code Server License Terms](https://aka.ms/vscode-server-license) and the [Microsoft Privacy Statement](https://privacy.microsoft.com/en-US/privacystatement).
>
> Some VS Code Server options (such as `--bind-addr` and `--auth`) may be ignored depending on the server version. The server will still be accessible on the default port (usually 8000).

---

## Directory Structure

```
ros2_yocto_project/
├── docker/
│   └── Dockerfile.yocto
├── README.md
└── ...
```

