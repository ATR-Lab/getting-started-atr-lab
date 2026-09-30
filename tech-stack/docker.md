# Docker

> **Read this when** you want to run ROS 2, a simulator or training code in a container, give a container a GPU or a window, or set up ROSEnv.

Docker runs software in containers: isolated copies of an operating system and its packages that start in seconds and behave the same on every machine. The lab uses containers so that a project's ROS 2 distribution, CUDA version and Python packages don't fight with everyone else's on shared machines. The one thing to remember: on a Linux machine with an NVIDIA GPU, use **Docker Engine plus the NVIDIA Container Toolkit**, not Docker Desktop.

## Contents

- [Words you will see](#words-you-will-see)
- [Docker Engine or Docker Desktop](#docker-engine-or-docker-desktop)
- [Install Docker Engine on Ubuntu](#install-docker-engine-on-ubuntu)
- [Give containers a GPU](#give-containers-a-gpu)
- [Run GUI apps from a container](#run-gui-apps-from-a-container)
- [Docker Compose](#docker-compose)
- [ROSEnv for ROS 2 projects](#rosenv-for-ros-2-projects)
- [Troubleshooting](#troubleshooting)
- [Related](#related)

## Words you will see

| Term | Meaning |
| --- | --- |
| Image | A read-only template: an operating system plus installed software, for example `osrf/ros:jazzy-desktop` |
| Container | A running copy of an image. Changes inside it disappear when you delete it, unless you save them in a volume |
| Volume or bind mount | A folder shared between your machine and the container, so your code and data survive |
| Dockerfile | A recipe that builds an image, step by step |
| Compose file | A YAML file (`compose.yaml`) that starts one or more containers with all their options |

## Docker Engine or Docker Desktop

| | Docker Engine | Docker Desktop |
| --- | --- | --- |
| What it is | The container runtime itself, open source ([Moby project](https://github.com/moby/moby), Apache 2.0) | An app that runs Docker Engine inside a virtual machine, with a GUI |
| Runs on | Linux | macOS, Windows, Linux |
| NVIDIA GPUs | Yes, with the [NVIDIA Container Toolkit](#give-containers-a-gpu) | Only on Windows with the WSL 2 backend ([Docker docs](https://docs.docker.com/desktop/features/gpu/)) |
| Use it in the lab for | Lab workstations and GPU servers (Ubuntu) | Your own Mac or Windows laptop, for work without a GPU |

On Linux, Docker Desktop runs its own virtual machine with a separate `desktop-linux` context, so images you pulled with Docker Engine do not show up in it ([Docker docs](https://docs.docker.com/desktop/setup/install/linux/)). Pick one per machine. Apple silicon Macs have no NVIDIA GPU, so CUDA containers do not run there.

> [!IMPORTANT]
> **Docker Desktop licensing is a lab decision.** Docker's [Desktop license page](https://docs.docker.com/subscription/desktop-license/) lists education among free uses, but its [subscription service agreement](https://www.docker.com/legal/docker-subscription-service-agreement/) (updated Aug. 26, 2026) says U.S. public education entities are covered by a separate public-sector agreement and are not entitled to the no-fee services, and that a research group sharing a project needs a paid institutional plan. Before you install Docker Desktop on a lab or university machine, ask [lab manager name] whether the lab has a license. Docker Engine on Linux is not affected.

## Install Docker Engine on Ubuntu

For Ubuntu 22.04, 24.04 and 26.04 LTS on x86_64 or arm64, from Docker's [Ubuntu install guide](https://docs.docker.com/engine/install/ubuntu/) (checked Sept. 30, 2026). If the machine already has Docker from Ubuntu's own packages (`docker.io`), remove it first:

```bash
sudo apt remove $(dpkg --get-selections docker.io docker-compose docker-compose-v2 docker-doc docker-buildx podman-docker containerd runc | cut -f1)
```

Add Docker's apt repository:

```bash
# Add Docker's official GPG key
sudo apt update
sudo apt install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to apt sources
sudo tee /etc/apt/sources.list.d/docker.sources <<EOF
Types: deb
URIs: https://download.docker.com/linux/ubuntu
Suites: $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}")
Components: stable
Architectures: $(dpkg --print-architecture)
Signed-By: /etc/apt/keyrings/docker.asc
EOF
sudo apt update
```

Install Docker Engine, Buildx and the Compose plugin, then test:

```bash
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo docker run hello-world
```

Docker's convenience script (`get.docker.com`) also works, but Docker says it "isn't recommended for production environments" and may upgrade Docker by a major version without warning. Use the apt repository on shared machines.

> [!WARNING]
> Ports you publish from a container (`-p 8080:8080`) bypass Ubuntu's firewall rules, so a service in a container can be reachable from the campus network. Publish only what you need, bound to `127.0.0.1` where you can (`-p 127.0.0.1:8080:8080`).

### Run Docker without sudo (your own machine)

```bash
sudo groupadd docker
sudo usermod -aG docker $USER
# Log out and back in (or run: newgrp docker), then check
docker run hello-world
```

> [!CAUTION]
> "The docker group grants root-level privileges to the user" ([Docker post-install guide](https://docs.docker.com/engine/install/linux-postinstall/)). On shared lab machines, only [machine administrator] adds people to the `docker` group.

## Give containers a GPU

The [NVIDIA Container Toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) lets containers use the host's NVIDIA GPU. It needs a working NVIDIA driver on the host (`nvidia-smi` must work outside Docker). Commands for Ubuntu, from NVIDIA's guide (version 1.20.1, checked Sept. 30, 2026):

```bash
sudo apt-get update && sudo apt-get install -y --no-install-recommends ca-certificates curl gnupg2

# Add NVIDIA's repository and signing key
curl -fsSL https://nvidia.github.io/libnvidia-container/gpgkey | sudo gpg --dearmor -o /usr/share/keyrings/nvidia-container-toolkit-keyring.gpg \
  && curl -s -L https://nvidia.github.io/libnvidia-container/stable/deb/nvidia-container-toolkit.list | \
    sed 's#deb https://#deb [signed-by=/usr/share/keyrings/nvidia-container-toolkit-keyring.gpg] https://#g' | \
    sudo tee /etc/apt/sources.list.d/nvidia-container-toolkit.list
sudo apt-get update

# Install a pinned version (check NVIDIA's guide for the current one)
export NVIDIA_CONTAINER_TOOLKIT_VERSION=1.20.1-1
sudo apt-get install -y \
    nvidia-container-toolkit=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
    nvidia-container-toolkit-base=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
    libnvidia-container-tools=${NVIDIA_CONTAINER_TOOLKIT_VERSION} \
    libnvidia-container1=${NVIDIA_CONTAINER_TOOLKIT_VERSION}

# Register the NVIDIA runtime with Docker and restart it
sudo nvidia-ctk runtime configure --runtime=docker
sudo systemctl restart docker
```

Test it with NVIDIA's [sample workload](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/sample-workload.html). You should see the same GPU table that `nvidia-smi` prints on the host:

```bash
sudo docker run --rm --runtime=nvidia --gpus all ubuntu nvidia-smi
```

## Run GUI apps from a container

RViz, Gazebo and rqt need a window on your screen. On Ubuntu with an X11 session, share the X server socket and your `DISPLAY` with the container. This follows the ROS 2 documentation's [VS Code and Docker guide](https://docs.ros.org/en/jazzy/How-To-Guides/Setup-ROS-2-with-VSCode-and-Docker-Container.html):

```bash
# Allow local containers to open windows on your display (undo later with: xhost -local:)
xhost +local:
docker run -it --rm \
  --net=host \
  -e DISPLAY=$DISPLAY \
  -v /tmp/.X11-unix:/tmp/.X11-unix \
  --device /dev/dri \
  osrf/ros:jazzy-desktop \
  rviz2
```

> [!WARNING]
> `xhost +local:` lets every local process, including every container, draw on and read from your screen. Run `xhost -local:` when you are done, and never run `xhost +` (no argument), which opens your display to the network. The ROS wiki's [GUI tutorial](https://wiki.ros.org/docker/Tutorials/GUI) (written for ROS 1) shows narrower options, such as allowing only one container's hostname.

For GPU-accelerated windows (Isaac Sim, Gazebo with an NVIDIA GPU), add `--gpus all` and `-e NVIDIA_DRIVER_CAPABILITIES=all` to the same command.

## Docker Compose

Compose saves a long `docker run` command as a file, so the whole team starts the container the same way. Compose ships as the `docker compose` plugin (two words; the old Python `docker-compose` is retired). An example `compose.yaml` for a ROS 2 container with a GPU and a display:

```yaml
services:
  ros:
    image: osrf/ros:jazzy-desktop
    network_mode: host
    environment:
      - DISPLAY=${DISPLAY}
    volumes:
      - /tmp/.X11-unix:/tmp/.X11-unix
      - ./ws:/ws            # your workspace, shared with the container
    working_dir: /ws
    command: sleep infinity
    deploy:
      resources:
        reservations:
          devices:
            - driver: nvidia
              count: 1
              capabilities: [gpu]
```

```bash
docker compose up -d          # start in the background
docker compose exec ros bash  # open a shell inside it
docker compose down           # stop and remove it
```

The GPU block follows Docker's [Compose GPU guide](https://docs.docker.com/compose/how-tos/gpu-support/); delete it on machines without an NVIDIA GPU.

## ROSEnv for ROS 2 projects

[ROSEnv](https://github.com/MarcoDotIO/rosenv) is an open-source ROS 2 project and dependency manager written by a lab member. You choose a ROS 2 distribution, declare packages in `rosenv.toml`, commit a `rosenv.lock` lockfile and run the workspace in a persistent Docker environment, so everyone on a project gets the same packages without installing ROS 2 on the host. It is MIT-licensed and not yet published as a release (version 0.2.0 on its main branch, Sept. 30, 2026).

It needs Linux (Ubuntu 24.04 is the tested host), Python 3.11 or later and a running Docker Engine. Install from source with [uv](https://docs.astral.sh/uv/) (or `pipx install .`):

```bash
git clone https://github.com/MarcoDotIO/rosenv.git
cd rosenv
uv tool install .
rosenv doctor
```

Start a project and run a node, from the ROSEnv README:

```bash
rosenv init --ros jazzy
rosenv add demo_nodes_cpp apt:git
rosenv run -- ros2 run demo_nodes_cpp talker
```

On another machine, `rosenv sync --locked` recreates the same environment from the lockfile, and `rosenv build` and `rosenv test` run colcon inside it. ROSEnv supports Humble, Jazzy (the default), Kilted, Lyrical and Rolling.

> [!NOTE]
> This version of ROSEnv does not pass GPUs, GUI windows or USB devices through to the container, so use plain Docker (above) for RViz, Gazebo, Isaac Sim or robots on a USB cable. Check the [ROSEnv README](https://github.com/MarcoDotIO/rosenv#readme) for changes.

The full ROS 2 guide, including when to use ROSEnv and when to install natively, is in [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2).

## Troubleshooting

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| `permission denied ... /var/run/docker.sock` | Your user is not in the `docker` group | Use `sudo`, or ask [machine administrator] to add you, then log out and back in |
| `could not select device driver "" with capabilities: [[gpu]]` | The NVIDIA Container Toolkit is missing or Docker was not restarted | Install the toolkit, run `sudo nvidia-ctk runtime configure --runtime=docker`, restart Docker |
| `cannot open display` or `could not connect to display` | The container has no access to your X server | Run `xhost +local:`, pass `-e DISPLAY=$DISPLAY` and mount `/tmp/.X11-unix` |
| Images you built are missing | Docker Desktop and Docker Engine keep separate image stores | Use one of them; check `docker context ls` |
| The disk is full | Old images, containers and build cache | `docker system df` shows usage; `docker image prune` removes unused images |

## Related

- [Tech stack](README.md): where Docker fits
- [Isaac Sim and Isaac Lab](isaac-sim.md): NVIDIA's simulator, which also ships as a container
- [Shared machines and GPUs](../lab-rules/best-practices.md#shared-machines-and-gpus)
- [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2): installing ROS 2 natively or with ROSEnv
- [Dev guidelines](https://github.com/ATR-Lab/dev-guidelines)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/tech-stack/docker.md)</sub>
