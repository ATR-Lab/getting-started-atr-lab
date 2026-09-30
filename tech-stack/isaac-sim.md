# Isaac Sim and Isaac Lab

> **Read this when** you need a photorealistic robot simulator, want to train a locomotion or manipulation policy with reinforcement learning, or want to test ROS 2 code against a simulated Unitree Go2 or SO-101.

[Isaac Sim](https://github.com/isaac-sim/IsaacSim) is NVIDIA's robot simulator, built on Omniverse: it renders cameras and lidars with ray tracing, simulates physics on the GPU and talks to ROS 2. [Isaac Lab](https://github.com/isaac-sim/IsaacLab) is the robot-learning framework on top of it, used to train policies across thousands of simulated robots at once. The one thing to remember: Isaac Sim needs an NVIDIA RTX GPU with at least 16 GB of memory, so most laptops cannot run it; use a lab workstation.

## Contents

- [Versions](#versions)
- [System requirements](#system-requirements)
- [Install Isaac Sim](#install-isaac-sim)
- [ROS 2 bridge](#ros-2-bridge)
- [Robot assets for lab robots](#robot-assets-for-lab-robots)
- [Isaac Lab](#isaac-lab)
- [Lab notes](#lab-notes)
- [Related](#related)

## Versions

Checked on Sept. 30, 2026:

| Package | Current version | Notes |
| --- | --- | --- |
| Isaac Sim | **6.1.0** (Sept. 10, 2026) | [Release notes](https://github.com/isaac-sim/IsaacSim/releases). A 7.0.0 alpha is out as a pre-release; don't use it for research runs |
| Isaac Lab | **3.0.0 early access** (Sept. 16, 2026), built for Isaac Sim 6.1 | NVIDIA targets general availability for the end of October 2026. The last stable line, **2.3.2**, works with Isaac Sim 4.5, 5.0 and 5.1 ([releases](https://github.com/isaac-sim/IsaacLab/releases)) |

Isaac Sim's source code is on GitHub under the Apache 2.0 license; running it also uses NVIDIA components under NVIDIA's [additional software license](https://www.nvidia.com/en-us/agreements/enterprise-software/isaac-sim-additional-software-and-materials-license/). You accept the Omniverse license agreement the first time you launch it. Isaac Lab is BSD-3-Clause.

## System requirements

From NVIDIA's [requirements page](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/requirements.html) for x86_64 machines:

| | Minimum | Good | Ideal |
| --- | --- | --- | --- |
| Operating system | Ubuntu 22.04 or 24.04, Windows 11 | Same | Same |
| GPU | GeForce RTX 4080 | GeForce RTX 5080 | RTX PRO 6000 Blackwell |
| GPU memory | 16 GB | 16 GB | 48 GB |
| RAM | 32 GB | 64 GB | 64 GB |
| CPU cores | 4 | 8 | 16 |
| Storage | 50 GB SSD | 500 GB SSD | 1 TB NVMe SSD |
| NVIDIA driver | Linux 595.58.03, Windows 595.97 | | |

GPUs without RT cores, such as the A100 and H100 data-center GPUs, are not supported. Isaac Sim does not run on macOS.

## Install Isaac Sim

There are four ways, all documented in the [installation guide](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/index.html). For most lab work, use pip in a virtual environment or the container.

**pip** (Ubuntu 22.04 or 24.04 with GLIBC 2.35 or later; needs Python 3.12):

```bash
python3.12 -m venv env_isaacsim
source env_isaacsim/bin/activate
pip install isaacsim[all,extscache]==6.1.0.0 --extra-index-url https://pypi.nvidia.com
# First launch: accept the license agreement when asked (or set OMNI_KIT_ACCEPT_EULA=YES)
isaacsim
```

**Container** (Ubuntu with Docker Engine and the [NVIDIA Container Toolkit](docker.md#give-containers-a-gpu)); follow the [container guide](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/install_container.html) for the volume mounts that cache shaders between runs:

```bash
docker pull nvcr.io/nvidia/isaac-sim:6.1.0
```

**Workstation download:** a zip for Linux or Windows from the [download page](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/download.html).

**From source:** clone [isaac-sim/IsaacSim](https://github.com/isaac-sim/IsaacSim) and run `build.sh`. It needs GCC 11, including on Ubuntu 24.04.

## ROS 2 bridge

"For the ROS 2 bridge, Isaac Sim is compatible with ROS 2 Humble and ROS 2 Jazzy" ([ROS installation guide](https://docs.isaacsim.omniverse.nvidia.com/latest/installation/install_ros.html)):

| Host | ROS 2 distribution |
| --- | --- |
| Ubuntu 24.04 | Jazzy (recommended) |
| Ubuntu 22.04 | Humble; Jazzy only if you build it from source |
| Windows 11 | Jazzy, installed through Pixi |

Kilted and Lyrical are not supported by this release. Isaac Sim ships its own internal ROS 2 libraries, so custom message packages must be built with Python 3.12 to load. For the lab's ROS 2 setup, see [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2).

## Robot assets for lab robots

Isaac Sim's asset library includes ready-made models ([quadrupeds](https://docs.isaacsim.omniverse.nvidia.com/latest/assets/usd_assets_robots_quadruped.html), [humanoids](https://docs.isaacsim.omniverse.nvidia.com/latest/assets/usd_assets_robots_humanoid.html), [manipulators](https://docs.isaacsim.omniverse.nvidia.com/latest/assets/usd_assets_robots_manipulator.html)). Checked against the lab's robots on Sept. 30, 2026:

| Lab robot | In the Isaac Sim library? | Asset path or note |
| --- | --- | --- |
| Unitree Go2 | Yes | `Unitree/Go2/go2.usd` |
| Booster K1 | No | Only the Booster T1 (`BoosterRobotics/BoosterT1/T1_locomotion.usd`); import a K1 model from URDF |
| LeRobot SO-101 | Yes | `RobotStudio/so101_new_calib/so101_new_calib.usd` |
| ROBOTIS OpenManipulator-X | No | Import from the manufacturer's URDF |

To bring in a robot that is not in the library, use the URDF importer (Isaac Sim converts URDF to USD, Omniverse's scene format). Meshes exported from Fusion work too; see [Autodesk Fusion and Inventor](autodesk.md#from-cad-to-simulation).

## Isaac Lab

Isaac Lab trains policies with reinforcement learning or imitation learning across many parallel simulated robots on one GPU. It needs at least 32 GB of RAM and 16 GB of GPU memory and runs on Ubuntu 22.04 or later or Windows 11 ([installation guide](https://isaac-sim.github.io/IsaacLab/release/3.0.0/source/setup/installation/index.html)).

- **Which version:** for a project starting now, ask your mentor. Version 3.0 is the one built for Isaac Sim 6.1 but is still early access; version 2.3.2 is stable but needs Isaac Sim 5.1 or older.
- **Install:** the 3.0 guide recommends [uv](https://docs.astral.sh/uv/); a pip wheel, Docker and source installs are also documented. Follow the guide for your chosen version rather than copying commands between versions.
- **Unitree Go2 tasks:** Isaac Lab ships flat- and rough-terrain velocity-tracking tasks for the Go2. Their names changed between versions: `Isaac-Velocity-Rough-Unitree-Go2-v0` in 2.3.2 and `Isaac-Velocity-Rough-UnitreeGo2` in 3.0 early access. Isaac Lab has no Booster robot configuration.

> [!WARNING]
> A policy trained in simulation can behave very differently on the real robot (the "sim-to-real gap"). Before a trained policy runs on the Go2 or any other robot, follow the robot's [safety section](../hardware/unitree-go2.md#safety) and the general rules for [robots in motion](../lab-rules/safety.md#robots-in-motion), and label any video of it as autonomous.

## Lab notes

- Machines that can run Isaac Sim: [list of lab workstations with RTX GPUs].
- Book GPU time before long training runs: [GPU booking method] ([shared machines and GPUs](../lab-rules/best-practices.md#shared-machines-and-gpus)).
- Shared Isaac Sim assets and lab robot models: [shared asset location].

## Related

- [Tech stack](README.md)
- [MuJoCo](mujoco.md) and [Gazebo](gazebo.md): other simulators the lab uses
- [Docker](docker.md): the NVIDIA Container Toolkit for the Isaac Sim container
- [LeRobot](lerobot.md): imitation learning on real arms
- [Unitree Go2](../hardware/unitree-go2.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/tech-stack/isaac-sim.md)</sub>
