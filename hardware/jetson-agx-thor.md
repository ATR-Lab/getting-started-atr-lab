# NVIDIA Jetson AGX Thor

> **Read this when** you are about to set up, use or check out the lab's NVIDIA Jetson AGX Thor Developer Kit for on-robot AI, containers or Isaac ROS.

This page covers the Jetson AGX Thor Developer Kit: its specs, how to install JetPack, power modes, running GPU containers and which ROS 2 and Isaac ROS versions work on it. The one thing to remember: **JetPack 7 runs Ubuntu 24.04**, so plain ROS 2 Jazzy installs from the standard packages, while the newest Isaac ROS (5.0) uses ROS 2 Lyrical from NVIDIA's own package repository. Pick one stack per project and write it down.

## Contents

- [Overview](#overview)
- [Key specs](#key-specs)
- [In our lab](#in-our-lab)
- [First steps](#first-steps)
- [Software](#software)
- [Safety](#safety)
- [Troubleshooting](#troubleshooting)
- [Resources](#resources)
- [Related](#related)

## Overview

The **NVIDIA Jetson AGX Thor Developer Kit** ([product page](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-thor/)) is a compact computer for robots, built on NVIDIA's Jetson T5000 module. It pairs an Arm CPU with a Blackwell GPU and 128 GB of memory, so large AI models (vision, language and robot policies) can run on the robot instead of in the cloud. It runs NVIDIA's JetPack software: Jetson Linux (Ubuntu 24.04), CUDA, TensorRT and container tools.

What the lab uses it for: `[current Jetson AGX Thor projects and who leads them]`.

## Key specs

From NVIDIA's [Jetson Thor product page](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-thor/) (Developer Kit column) and the [developer kit user guide](https://docs.nvidia.com/jetson/agx-thor-devkit/user-guide/latest/index.html), checked Sept. 30, 2026.

| Spec | Jetson AGX Thor Developer Kit |
| --- | --- |
| Module | Jetson T5000 |
| AI performance | 2070 TFLOPS (FP4, sparse) |
| GPU | 2560-core NVIDIA Blackwell GPU with fifth-generation Tensor Cores; Multi-Instance GPU with 10 TPCs; up to 1.57 GHz |
| CPU | 14-core Arm Neoverse-V3AE (64-bit), up to 2.6 GHz |
| Memory | 128 GB 256-bit LPDDR5X, 273 GB/s |
| Storage | 1 TB NVMe SSD in an M.2 Key M slot (pre-installed) |
| Module power | 40-130 W |
| Networking | 1 × 5GbE RJ45; 1 × QSFP28 (4 × 25GbE); Wi-Fi 6E |
| Display | 1 × HDMI 2.0b, 1 × DisplayPort 1.4a |
| USB | 2 × USB-A (3.2 Gen2), 2 × USB-C (3.1), plus a debug USB-C port |
| Cameras | Holoscan Sensor Bridge cameras through the QSFP port; USB cameras |
| Other I/O | CAN headers, automation header, PWM fan connector, RTC battery connector |
| Power input | Included 140 W USB-C power supply (28 V × 5 A) into either main USB-C port |
| Size | 243.19 × 112.40 × 56.88 mm |
| Operating temperature | 0 °C to 35 °C ([carrier board specification, PDF](https://developer.nvidia.com/downloads/assets/embedded/secure/jetson/thor/docs/jetson-thor-developer-kit-carrier-board-specification.pdf)) |

## In our lab

| Item | Details |
| --- | --- |
| Quantity | `[N]` |
| Location | `[Room ###, bench, rack or robot it is mounted on]` |
| Owner or contact | `[Jetson AGX Thor owner or contact name]` |
| Checkout | `[checkout procedure]` |
| Installed JetPack and power mode | `[JetPack version; nvpmodel mode]` |
| Accounts and credentials | The Ubuntu login and NGC API key: ask `[lab manager name]`; never commit them to any repo |
| Lab repos | `[lab repos that target the Thor, if any are public]` |

## First steps

NVIDIA's [quick start](https://docs.nvidia.com/jetson/agx-thor-devkit/user-guide/latest/quick_start.html) installs the operating system from a USB stick, with no second Ubuntu computer needed. On Sept. 30, 2026 the latest release for the kit was **JetPack 7.2.1** with Jetson Linux 39.2.1 ([JetPack downloads](https://developer.nvidia.com/embedded/jetpack/downloads)). Reinstalling erases the kit, so ask `[Jetson AGX Thor owner or contact name]` before you do it.

1. Finish the [hardware checklist](README.md#before-you-use-any-hardware).
2. On any computer with at least 25 GB free, download the Jetson ISO image from the [JetPack downloads page](https://developer.nvidia.com/embedded/jetpack/downloads) and write it to a USB stick of 16 GB or more with Balena Etcher.
3. Connect a monitor (HDMI or DisplayPort), a USB keyboard and mouse, and the USB stick. Plug the **included** power supply into one of the two main USB-C ports and press the power button (the left button).
4. If a firmware (QSPI capsule) update prompt appears, press <kbd>Y</kbd>; the kit updates and restarts.
5. In the installer menu, choose **Install on NVMe**. Installation takes about 10 minutes.
6. Remove the USB stick, reboot and finish Ubuntu's first-boot setup (user account, language, network).
7. Install the JetPack components (CUDA, TensorRT and more; they need more than 15 GB) ([JetPack setup](https://docs.nvidia.com/jetson/agx-thor-devkit/user-guide/latest/setup_jetpack.html)):

   ```bash
   # On the Thor, JetPack 7.2.1 (Ubuntu 24.04)
   sudo apt update
   sudo apt install nvidia-jetpack
   ```

8. Check the installed Jetson Linux release (it reports R39 on JetPack 7.2.x):

   ```bash
   # On the Thor
   cat /etc/nv_tegra_release
   ```

NVIDIA also documents flashing with SDK Manager or the Linux_for_Tegra flash scripts from an Ubuntu host ([BSP setup](https://docs.nvidia.com/jetson/agx-thor-devkit/user-guide/latest/setup_bsp.html)). Moving to Jetson Linux 39.2.x is not supported as an `apt` upgrade: you reinstall. A kit whose firmware was updated to 39.2.x can't boot older installer images ([compatibility note](https://docs.nvidia.com/jetson/agx-thor-devkit/user-guide/latest/twa_uefi_iso_compatibility.html)).

## Software

### Power modes

The power mode (set with `nvpmodel`) caps how much power the module may use. From NVIDIA's [power management guide for Jetson Thor](https://docs.nvidia.com/jetson/archives/r39.2.1/DeveloperGuide/SD/PlatformPowerAndPerformance/JetsonThor.html):

| Mode ID | Name | CPU cores online | GPU TPCs | GPU maximum clock |
| --- | --- | --- | --- | --- |
| 0 | MAXN (no fixed power budget) | 14 | 10 | 1575 MHz |
| 1 | 120W (**default**) | 14 | 10 | 1386 MHz |
| 2 | 90W | 12 | 6 | 1530 MHz |
| 3 | 70W | 12 | 6 | 1530 MHz |

```bash
# On the Thor (JetPack 7.2.1): show the current power mode
sudo /usr/sbin/nvpmodel -q
# Switch to mode 1 (120W); some changes ask for a reboot
sudo /usr/sbin/nvpmodel -m 1
# Show, then pin, clocks at their maximum for the current mode
sudo /usr/bin/jetson_clocks --show
sudo /usr/bin/jetson_clocks
# Live CPU, GPU, memory, power and temperature readout
sudo tegrastats
```

NVIDIA describes MAXN as an unconstrained mode in which hardware throttling can still kick in, and points to its thermal design guide before running heavy workloads in it. The mode you set survives reboots, so set it back to `[lab default power mode]` when you finish.

### Containers

JetPack 7 on Thor follows NVIDIA's server-style (SBSA) software stack, so it runs the regular multi-architecture NVIDIA GPU Cloud (NGC) containers rather than Jetson-only images ([JetPack page](https://developer.nvidia.com/embedded/jetpack)). The USB-stick install already includes Docker and the NVIDIA Container Toolkit ([Docker setup](https://docs.nvidia.com/jetson/agx-thor-devkit/user-guide/latest/setup_docker.html)). NVIDIA's test from that page:

```bash
# On the Thor (JetPack 7.2.1), from the folder you want mounted as /workspace
docker run --rm -it \
    -v "$PWD":/workspace \
    -w /workspace \
    nvcr.io/nvidia/pytorch:25.08-py3
```

Inside the container, `torch.cuda.get_device_name(0)` should report `NVIDIA Thor`. Newer NGC tags exist, but NVIDIA's Thor guide only demonstrates `25.08-py3`; check a tag's release notes for Thor before you rely on it. The [jetson-containers](https://github.com/dusty-nv/jetson-containers) project also lists JetPack 7 support. Lab guide: [Docker](../tech-stack/docker.md).

### ROS 2 and Isaac ROS

| Option | ROS 2 distro | Notes |
| --- | --- | --- |
| Upstream ROS 2 | Jazzy | Tier 1 on Ubuntu 24.04 arm64 ([REP 2000](https://reps.openrobotics.org/rep-2000/)); supported until May 2029 |
| Isaac ROS 5.0.0 (Sept. 21, 2026) | Lyrical | "Migrated to ROS 2 Lyrical Luth"; installs Lyrical for Ubuntu 24.04 from NVIDIA's Isaac ROS Buildfarm repository, because upstream Lyrical targets Ubuntu 26.04. Removed the NITROS packages ([release notes](https://nvidia-isaac-ros.github.io/releases/index.html)) |
| Isaac ROS 4.6.0 (Aug. 18, 2026) | Jazzy | Added JetPack 7.2 support ([4.6 getting started](https://nvidia-isaac-ros.github.io/v/release-4.6/getting_started/index.html)) |

Isaac ROS 5.0 lists "Jetson Thor (T5000 and T4000)" with **JetPack 7.2** and a 128 GB or larger NVMe drive ([getting started](https://nvidia-isaac-ros.github.io/getting_started/index.html)); its setup steps also set the power mode to MAXN. Check the release notes before pairing it with JetPack 7.2.1. Lab guides: [ROS 2](../tech-stack/ros2.md), [Isaac Sim](../tech-stack/isaac-sim.md) and the lab-robots page in [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md).

## Safety

Read the lab's [safety rules](../lab-rules/safety.md) first, including [workbench and electronics](../lab-rules/safety.md#workbench-and-electronics). The Thor has no moving parts except its fan, but it draws up to 140 W and runs hot.

> [!WARNING]
> **Use the included 140 W power supply.** NVIDIA "strongly recommended" the bundled USB-C supply ([quick start](https://docs.nvidia.com/jetson/agx-thor-devkit/user-guide/latest/quick_start.html)) and says performance and stability are not guaranteed with another adapter. Never raise the current or power limits in software: NVIDIA's [power guide](https://docs.nvidia.com/jetson/archives/r39.2.1/DeveloperGuide/SD/PlatformPowerAndPerformance/JetsonThor.html) warns this can cause permanent damage.

- **Static.** The carrier board has electrostatic-sensitive parts. Touch a grounded surface before handling it, and connect cables and peripherals before you connect power ([carrier board specification](https://developer.nvidia.com/downloads/assets/embedded/secure/jetson/thor/docs/jetson-thor-developer-kit-carrier-board-specification.pdf)).
- **Heat.** Keep the fan and vents clear, and run it within 0 °C to 35 °C. Check temperatures with `tegrastats` during long jobs.
- **On a robot.** When the Thor rides on a robot, mount it firmly, route the power cable away from moving joints and follow the robot's own page in this folder.

## Troubleshooting

| Problem | What to try | Source |
| --- | --- | --- |
| No picture through a KVM switch or adapter | Connect the monitor directly | [Quick start](https://docs.nvidia.com/jetson/agx-thor-devkit/user-guide/latest/quick_start.html) |
| An older installer USB stick won't boot | Firmware 39.2.x can't boot older ISOs; use the current ISO | [Compatibility note](https://docs.nvidia.com/jetson/agx-thor-devkit/user-guide/latest/twa_uefi_iso_compatibility.html) |
| Some USB-C devices (for example RealSense cameras) aren't detected | A known issue in Jetson Linux 39.2.1; the release notes give a workaround | [Release notes, PDF](https://docs.nvidia.com/jetson/archives/r39.2.1/ReleaseNotes/Jetson_Linux_Release_Notes_r39.2.1.pdf) |
| A power-mode change didn't take effect | Modes that change the GPU layout, or changes after `jetson_clocks`, need a reboot | [Power guide](https://docs.nvidia.com/jetson/archives/r39.2.1/DeveloperGuide/SD/PlatformPowerAndPerformance/JetsonThor.html) |
| You need to reflash from a host computer | Enter Force Recovery mode: hold the Force Recovery button (middle), press Reset (right), release Force Recovery | [Hardware layout](https://docs.nvidia.com/jetson/agx-thor-devkit/user-guide/latest/hardware_layout.html) |
| Anything else | Search the Jetson Thor forum, where NVIDIA staff answer | [Jetson Thor forum](https://forums.developer.nvidia.com/c/robotics-edge-computing/jetson-systems/jetson-thor/740) |

## Resources

- Official: [product page](https://www.nvidia.com/en-us/autonomous-machines/embedded-systems/jetson-thor/) · [developer kit user guide](https://docs.nvidia.com/jetson/agx-thor-devkit/user-guide/latest/index.html) · [JetPack](https://developer.nvidia.com/embedded/jetpack) and [downloads](https://developer.nvidia.com/embedded/jetpack/downloads) · [Jetson Linux 39.2.1 release notes (PDF)](https://docs.nvidia.com/jetson/archives/r39.2.1/ReleaseNotes/Jetson_Linux_Release_Notes_r39.2.1.pdf) · [power management for Jetson Thor](https://docs.nvidia.com/jetson/archives/r39.2.1/DeveloperGuide/SD/PlatformPowerAndPerformance/JetsonThor.html) · [Jetson Thor forum](https://forums.developer.nvidia.com/c/robotics-edge-computing/jetson-systems/jetson-thor/740)
- Software: [Isaac ROS](https://nvidia-isaac-ros.github.io/getting_started/index.html) · [NGC PyTorch container](https://catalog.ngc.nvidia.com/orgs/nvidia/containers/pytorch) · [jetson-containers](https://github.com/dusty-nv/jetson-containers)
- Lab: [lab robots and ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md)

## Related

- [Lab hardware index](README.md) and the [checklist before you use any hardware](README.md#before-you-use-any-hardware)
- [Raspberry Pi 5](raspberry-pi-5.md), the lab's small Linux computer
- [SO-101 arms](lerobot-so-101.md), whose policies can run on a GPU computer like this one
- [Lab safety rules](../lab-rules/safety.md)
- Tech stack: [Docker](../tech-stack/docker.md) · [ROS 2](../tech-stack/ros2.md) · [Isaac Sim](../tech-stack/isaac-sim.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/hardware/jetson-agx-thor.md)</sub>
