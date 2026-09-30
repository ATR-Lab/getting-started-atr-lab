# Raspberry Pi 5

> **Read this when** you are about to set up a lab Raspberry Pi 5 for a robot, sensor or ROS 2 project, or you need to pick its power supply, cooling, operating system or storage.

This page covers the Raspberry Pi 5: its specs, the power supply and cooling it needs, which operating system to install for ROS 2, how to boot from an NVMe drive and how to read its warning signs. The one thing to remember: **for ROS 2 Jazzy, install Ubuntu 24.04 LTS (64-bit)**, where Jazzy has official binary packages; on Raspberry Pi OS you would have to build ROS 2 from source or run it in a container.

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

The [Raspberry Pi 5](https://www.raspberrypi.com/products/raspberry-pi-5/) is a credit-card-sized Linux computer with a quad-core Arm CPU, PCIe for fast storage, two camera connectors and a 40-pin GPIO header for sensors and motor boards. Robots use it as an onboard computer for light workloads: running ROS 2 nodes, reading sensors, streaming a camera or bridging to a microcontroller. For heavy AI models, see the [Jetson AGX Thor](jetson-agx-thor.md).

What the lab uses it for: `[current Raspberry Pi 5 projects and who leads them]`.

## Key specs

From the [Raspberry Pi 5 product brief (PDF)](https://pip-assets.raspberrypi.com/categories/892-raspberry-pi-5/documents/RP-008348-DS-6-raspberry-pi-5-product-brief.pdf) (published April 2026) and the [product page](https://www.raspberrypi.com/products/raspberry-pi-5/), checked Sept. 30, 2026.

| Spec | Raspberry Pi 5 |
| --- | --- |
| Processor | Broadcom BCM2712, quad-core 64-bit Arm Cortex-A76 at 2.4 GHz; 512 KB L2 per core, 2 MB shared L3 |
| Graphics | VideoCore VII GPU (OpenGL ES 3.1, Vulkan) |
| Memory | LPDDR4X-4267: 1 GB, 2 GB, 4 GB, 8 GB or 16 GB |
| Video | Two 4Kp60 HDMI outputs with HDR; 4Kp60 HEVC decoder |
| USB | 2 × USB 3.0 (5 Gbps, at the same time), 2 × USB 2.0 |
| Networking | Gigabit Ethernet (PoE+ with a separate HAT); dual-band 802.11ac Wi-Fi; Bluetooth 5.0 and BLE |
| PCIe | PCIe 2.0 ×1 (needs the M.2 HAT+ or another adapter) |
| Cameras and displays | 2 × four-lane MIPI camera/display connectors |
| Storage | microSD slot (SDR104 high-speed mode); NVMe through PCIe |
| Other | Real-time clock (external battery), power button, 40-pin GPIO header, four-pin PWM fan connector |
| Power input | 5 V, 5 A over USB-C with USB Power Delivery |
| Operating temperature | 0 °C to 70 °C |
| Production lifetime | Until at least January 2036 |

## In our lab

| Item | Details |
| --- | --- |
| Quantity | `[N]`, with RAM sizes `[RAM per board]` |
| Location | `[Room ###, drawer or bin]` |
| Owner or contact | `[Raspberry Pi owner or contact name]` |
| Checkout | `[checkout procedure]` |
| Standard lab setup | `[OS image and version the lab uses, for example Ubuntu 24.04 with ROS 2 Jazzy]` |
| Accessories | `[27 W power supplies, Active Coolers, M.2 HAT+ boards, NVMe drives, cases]` |
| Accounts and credentials | Set your own user password when you flash the card, and ask `[lab manager name]` for Wi-Fi access. Never commit passwords, Wi-Fi keys or SSH keys to any repo |
| Lab repos | `[lab repos that run on the Pi 5, if any are public]` |

## First steps

1. Finish the [hardware checklist](README.md#before-you-use-any-hardware).
2. **Get the right power supply:** the Raspberry Pi 27 W USB-C Power Supply (5.1 V, 5 A). See [Power](#power-and-cooling).
3. **Fit a cooler:** the Raspberry Pi Active Cooler or the official case with its fan.
4. **Choose the operating system** (next section) and write it to a microSD card (or an NVMe drive) with [Raspberry Pi Imager](https://www.raspberrypi.com/software/). If Imager opens its Customisation tab for your OS, set the hostname, your username and password, Wi-Fi and remote access (SSH) there, so the Pi is reachable on first boot.
5. **Insert the card, connect the peripherals, then the power.** The power LED is red when power arrives, turns green during boot and stays green while running.
6. **Update it:**

   ```bash
   # Raspberry Pi OS or Ubuntu
   sudo apt update
   sudo apt full-upgrade
   ```

7. **Shut down properly** before you unplug it: `sudo shutdown now`, or press the power button once (on the desktop this opens a shutdown dialog).

## Software

### Choosing an operating system

| Operating system | Base | ROS 2 support | Use it when |
| --- | --- | --- | --- |
| **Ubuntu 24.04 LTS (64-bit)** | Ubuntu Noble | **ROS 2 Jazzy: Tier 1, official binary packages for arm64** ([REP 2000](https://reps.openrobotics.org/rep-2000/)). Jazzy is supported until May 2029 | Your project uses ROS 2 Jazzy (the lab's usual choice: `[confirm lab default distro]`) |
| Ubuntu 26.04 LTS (64-bit) | Ubuntu Resolute | ROS 2 Lyrical: Tier 1 for arm64 ([Lyrical platforms](https://docs.ros.org/en/lyrical/Releases/lyrical/supported-platforms.html)) | Your project has moved to Lyrical, released May 22, 2026 |
| Raspberry Pi OS (64-bit) | Debian 13 "trixie" (release of Sept. 15, 2026); a Debian 12 "bookworm" legacy image is still offered | No Tier 1 binaries: Jazzy supports Debian 12 at Tier 3 and Lyrical supports Debian 13 at Tier 3 (build from source). You can run ROS 2 in a Docker container instead | You need Raspberry Pi's own camera and GPIO tooling first, and ROS 2 second |

Sources: [Raspberry Pi OS downloads](https://www.raspberrypi.com/software/operating-systems/), [ROS 2 distributions](https://docs.ros.org/en/rolling/Releases.html). Ubuntu 24.04 was the first Ubuntu LTS to support the Pi 5 with arm64 server and desktop images ([Ubuntu 24.04 release notes](https://documentation.ubuntu.com/release-notes/24.04/)); the current 24.04.5 Pi images are at [cdimage.ubuntu.com](https://cdimage.ubuntu.com/releases/24.04/release/).

After Ubuntu 24.04 is running, install ROS 2 Jazzy with the official [Ubuntu (deb packages) guide](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html). Lab guides: [ROS 2](../tech-stack/ros2.md), [Docker](../tech-stack/docker.md) and the lab-robots page in [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md).

### Power and cooling

- **Power supply.** Raspberry Pi recommends its [27 W USB-C Power Supply](https://www.raspberrypi.com/products/27w-power-supply/) for the Pi 5 ([power supply docs](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#power-supply)). With a supply that can't deliver 5 A at 5 V, "the Raspberry Pi 5 restricts downstream USB devices to 600mA of power" (1.6 A with the right supply), and USB boot is off by default. The fan connector shares that USB current limit.
- **Undervoltage.** If the supply dips below 4.63 V (±5%), the Pi logs an undervoltage warning.
- **Cooling.** The Pi keeps its chip under 85 °C by slowing down: between 80 °C and 85 °C the CPU cores are throttled progressively, and at 85 °C the CPU and GPU both slow down. Use the [Active Cooler](https://www.raspberrypi.com/products/active-cooler/) or the [official case](https://www.raspberrypi.com/products/raspberry-pi-5-case/) with its fan: the fan starts at 50 °C and reaches full speed at 75 °C.

```bash
# Raspberry Pi OS: CPU temperature, and whether it has throttled or seen undervoltage
vcgencmd measure_temp
vcgencmd get_throttled
```

`get_throttled` returns a bit mask: `0x1` means undervoltage now, `0x4` throttled now, `0x10000` undervoltage has occurred and `0x40000` throttling has occurred since boot ([Raspberry Pi OS docs](https://www.raspberrypi.com/documentation/computers/os.html)).

### Storage: microSD or NVMe

- **microSD** is the default. Use a good-quality card and keep a backup image of a working setup.
- **NVMe** through the [M.2 HAT+](https://www.raspberrypi.com/documentation/accessories/m2-hat-plus.html) is faster and more reliable for logging. The M.2 HAT+ takes 2230 and 2242 drives (the Compact version only 2230), runs a single-lane PCIe 2.0 link and supplies up to 3 A to the drive.

To boot from NVMe (from the M.2 HAT+ guide):

1. Update the Pi's bootloader firmware first:

   ```bash
   # Raspberry Pi OS: check the current bootloader version
   sudo rpi-eeprom-update
   # In the menu, choose Advanced Options > Bootloader Version > Latest, then Finish
   sudo raspi-config
   # Install the latest bootloader
   sudo rpi-eeprom-update -a
   ```

2. Write the operating system to the NVMe drive with Raspberry Pi Imager.
3. With no microSD card inserted, the Pi 5 boots from NVMe. With a card inserted it tries the card first; change that in `sudo raspi-config` under Advanced Options, then Boot Order, then NVMe/USB boot.

## Safety

Read the lab's [safety rules](../lab-rules/safety.md) first, including [workbench and electronics](../lab-rules/safety.md#workbench-and-electronics). From the product brief's safety instructions and Raspberry Pi's documentation:

> [!WARNING]
> **Disconnect power before you connect or remove a HAT** or anything on the GPIO header. A slip across the pins while the Pi is powered can damage the board or the device you are wiring.

- **Power.** Use the 27 W supply (or another supply that meets the Pi 5's 5 V, 5 A requirement); undersized supplies cause undervoltage and USB problems.
- **Surface and airflow.** Run it on a stable, flat, non-conductive surface, in a well-ventilated place, and don't cover it while it runs.
- **Static.** Handle the board by its edges.
- **Water and heat.** Keep it away from liquids and heat sources.
- **On a robot.** Mount it firmly, and if it shares a battery with motors, power it through a regulator rated for 5 V and 5 A. Ask `[lab manager name]` before you wire a Pi to a robot battery.

## Troubleshooting

| Problem | What to try | Source |
| --- | --- | --- |
| USB devices disconnect or a drive won't power up | The supply isn't negotiating 5 A. Use the 27 W supply | [Power supply docs](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#power-supply) |
| `get_throttled` shows `0x1` or `0x10000` | Undervoltage: change the supply or cable | [Raspberry Pi OS docs](https://www.raspberrypi.com/documentation/computers/os.html) |
| Slow under load, `get_throttled` shows `0x4` or `0x40000` | Thermal throttling: fit the Active Cooler, clear the vents | [Thermal docs](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#frequency-management-and-thermal-control) |
| The power LED blinks a pattern and it won't boot | Count the long and short flashes: 0 long and 3 short is a generic boot failure; 0 and 7, kernel not found; 4 and 6 or 4 and 7, power failure. The full table is in the docs | [LED warning codes](https://www.raspberrypi.com/documentation/computers/configuration.html) |
| It won't boot from NVMe | Update the bootloader, check the boot order and check that the ribbon cable is fully and evenly seated at both ends | [M.2 HAT+ guide](https://www.raspberrypi.com/documentation/accessories/m2-hat-plus.html) |
| The bootloader seems corrupted | In Imager, write Misc utility images, then Bootloader, then SD Card Boot to a spare card, boot from it and wait for a steady green flash | [Bootloader recovery](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html) |

## Resources

- Official: [Raspberry Pi 5 product page](https://www.raspberrypi.com/products/raspberry-pi-5/) · [product brief (PDF)](https://pip-assets.raspberrypi.com/categories/892-raspberry-pi-5/documents/RP-008348-DS-6-raspberry-pi-5-product-brief.pdf) · [Raspberry Pi hardware docs](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html) · [Raspberry Pi OS](https://www.raspberrypi.com/software/operating-systems/) · [Raspberry Pi Imager](https://www.raspberrypi.com/software/) · [M.2 HAT+](https://www.raspberrypi.com/documentation/accessories/m2-hat-plus.html) · [forums](https://forums.raspberrypi.com/)
- Ubuntu and ROS 2: [Ubuntu for Raspberry Pi](https://ubuntu.com/download/raspberry-pi) · [ROS 2 Jazzy install (Ubuntu debs)](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html) · [REP 2000 platform tiers](https://reps.openrobotics.org/rep-2000/)
- Lab: [lab robots and ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md)

## Related

- [Lab hardware index](README.md) and the [checklist before you use any hardware](README.md#before-you-use-any-hardware)
- [Jetson AGX Thor](jetson-agx-thor.md), for heavier on-robot AI
- [ROSMASTER X3](rosmaster-x3.md), which can ship with a Raspberry Pi 5 as its main controller
- [Lab safety rules](../lab-rules/safety.md)
- Tech stack: [ROS 2](../tech-stack/ros2.md) · [Docker](../tech-stack/docker.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/hardware/raspberry-pi-5.md)</sub>
