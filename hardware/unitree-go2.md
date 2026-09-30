# Unitree Go2 Pro

> **Read this when** you are about to drive, program or check out the lab's Unitree Go2 Pro quadruped (a four-legged "robot dog").

This page covers what the Go2 Pro can and cannot do, how to power it on and connect to it, which software works with it and the safety rules for walking it. The one thing to remember: the **Pro model does not open Unitree's official developer interfaces** (the SDK and ROS 2 over DDS are EDU features), so programming our Pro goes through unofficial community tools that a firmware update can break.

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

The [Unitree Go2](https://www.unitree.com/go2/) is a battery-powered quadruped robot with 12 joint motors (three per leg), a 4D lidar in its head, an HD wide-angle camera and Wi-Fi 6 and Bluetooth radios. You drive it from the Unitree Go phone app or an optional handheld remote. Unitree sells it in four models: Air, Pro, X and EDU. **The lab's unit is a Go2 Pro.**

The Go2 is one of the lab's current research platforms. What we use it for right now: `[current Go2 projects and who leads them]`.

When you drive the Go2 with the app or the remote, it is **teleoperated**: you choose where it goes, and its onboard motion controller keeps it balanced and picks the foot placements. When a program you wrote sends it commands, the behavior is autonomous or semi-autonomous. Label every demo and video with which one it is.

### Air, Pro, X and EDU: what differs

Unitree's [product page](https://www.unitree.com/go2/) and its [About Go2 developer page](https://support.unitree.com/home/en/developer/about_Go2) compare the models. These are the rows that matter most in a lab:

| Feature | Air | Pro | X | EDU |
| --- | --- | --- | --- | --- |
| Secondary development (Unitree SDK, ROS 2 over DDS) | No | **No** | Basic support | Yes |
| Extended electrical interfaces (Ethernet RJ45, SBUS, 28.8 V power output) | No | **No** | No | Yes |
| High-compute expansion module (NVIDIA Jetson Orin, 40-100 TOPS) | No | **No** | No | Optional |
| Foot-end force sensors | No | **No** | No | Yes |
| Depth camera | No | **No** | No | Yes |
| Handheld remote controller | Optional | Optional | Included | Included |
| 4G module with GPS | No | Yes | Yes | Yes |
| Voice functions | No | Yes | Yes | Yes |
| Automatic retractable handle | No | Yes | No | No |
| Charging pile (dock) | No | No | Yes | Yes |
| Speed | 0-2.5 m/s | 0-3.5 m/s | 0-3.7 m/s | 0-3.7 m/s |
| Battery | 8,000 mAh | 8,000 mAh | 8,000 mAh | 15,000 mAh |

What this means for our Pro:

- Unitree's [developer FAQ](https://support.unitree.com/home/en/developer/FAQ) says "Only EDU or above versions can be developed" and that Pro and Air "do not open the secondary development interface".
- The same FAQ says the Go2 "only supports wired connection for development", and the About Go2 page says the Ethernet port is "exclusive to the Go2 EDU version". The Pro has no official way in.
- The official SDK and ROS 2 packages (below) are therefore **EDU-only**. Pro owners use community tools that speak the same WebRTC protocol as the phone app.

## Key specs

Values for the Pro, from the [Go2 product page](https://www.unitree.com/go2/) and the [About Go2 developer page](https://support.unitree.com/home/en/developer/about_Go2), checked Sept. 30, 2026. Unitree updates the Go2 line over time, so compare with the label and app readout of our unit.

| Spec | Go2 Pro |
| --- | --- |
| Size, standing | 70 × 31 × 40 cm |
| Size, crouching | 76 × 31 × 20 cm |
| Weight | About 15 kg with battery |
| Joint motors | 12 (12 degrees of freedom) |
| Maximum joint torque | About 45 N·m (largest joint motor) |
| Speed | 0-3.5 m/s |
| Payload | About 8 kg (maximum about 10 kg) |
| Maximum step height and slope | About 16 cm; 40° |
| Onboard computer | 8-core CPU (no expansion compute on the Pro) |
| Lidar | 4D lidar in the head. The current product page says LiDAR L2; older Unitree pages describe the L1. Check our unit |
| Camera | HD wide-angle camera in the head |
| Radios | Wi-Fi 6 (dual band), Bluetooth 5.2/4.2/2.1, 4G with GPS |
| Battery | 8,000 mAh, 236.8 Wh; runtime about 1-2 hours; charge time about 2 hours |
| Charger | 33.6 V, 3.5 A |
| Operating temperature | 5 °C to 35 °C, "in a good weather environment" |

## In our lab

| Item | Details |
| --- | --- |
| Quantity | `[N]` |
| Location | `[Room ###, shelf or cabinet]` |
| Owner or contact | `[Go2 owner or contact name]` |
| Checkout | `[checkout procedure]` |
| Handheld remote | `[whether our unit has the optional remote]` |
| Firmware version | `[current firmware version, from the app]` |
| Accounts and credentials | The robot is bound to a Unitree account. Ask `[lab manager name]` for access; never commit account details, Wi-Fi passwords or device keys to any repo |
| Lab repos | [ATR-Lab/go2_ws](https://github.com/ATR-Lab/go2_ws) (see below) |

**ATR-Lab/go2_ws.** Its README describes a ROS 2 workspace "for controlling and interacting with Unitree Go2 robot dogs" with these packages:

- `go2_robot_sdk`: communication with and control of the Go2.
- `test_camera` and `test_camera_ui`: camera capture and streaming, and a Qt video display.
- `human_interaction`: human detection and gesture recognition.
- `speech_processor`: audio processing and text-to-speech.
- `navigation_manager`: navigation and mapping.

The README also documents video-streaming fixes over WebRTC from January 2025. The workspace's `src/README.md` is the README of the community [go2_ros2_sdk](https://github.com/abizovnuralem/go2_ros2_sdk) project, so the driver builds on that project. The top-level README does not name a ROS 2 distro: ask `[go2_ws maintainer]` which one the lab uses.

## First steps

Do these with a trained lab member the first time. Unitree does not publish a Go2 user manual on its own site, so the power-button sequence comes from your training.

1. Finish the [hardware checklist](README.md#before-you-use-any-hardware) and read [Safety](#safety) below.
2. Install the **Unitree Go** app (iOS or Android, international version) from Unitree's [Go2 app page](https://www.unitree.com/app/go2/).
3. Ask `[lab manager name]` which Unitree account the robot is bound to and how to sign in. Don't bind the lab robot to a personal account.
4. Put the robot on flat, open floor in its **initial position** (lying down, legs folded). Unitree's [FAQ](https://support.unitree.com/home/en/developer/FAQ): "The Go2 does not support hanging and powering on".
5. Insert a charged battery and power on with `[power-on button sequence, from training]`.
6. Watch the status light ([About Go2](https://support.unitree.com/home/en/developer/about_Go2)):
   - Flashing green: switching on.
   - Steady green: powered on, default obstacle avoidance on.
   - Slow red flash: system abnormality, boot failure or hardware failure. Power off and tell `[lab manager name]`.
   - Fast red flash: motor and IMU calibration failed.
7. Turn on your phone's Bluetooth and connect in the app ([app binding guide](https://support.unitree.com/home/en/developer/App_binding)). Pick one mode:
   - **AP mode:** the robot makes its own hotspot, named `GO2-XXXXXX`.
   - **Wi-Fi (STA) mode:** the robot joins an existing network. The lab network is `[lab robot network]`.
8. If our unit has the handheld remote, pair it through the app ([Go2 control page](https://www.unitree.com/go2/control/)).
9. Check the firmware version in the app. **Do not install a firmware update** without asking `[lab manager name]`; updates have broken the community tools and lab code (see [Software](#software)).
10. When you finish, lie the robot down (remote: <kbd>L2</kbd> + <kbd>A</kbd>), power it off and return it and the battery as `[checkout procedure]` says.

## Software

### Official Unitree software

| Software | What it is | Works on our Pro? |
| --- | --- | --- |
| Unitree Go app | Phone app: driving, modes, settings, firmware updates | Yes |
| [unitree_sdk2](https://github.com/unitreerobotics/unitree_sdk2) | C++ SDK over DDS (BSD-3-Clause; README lists Ubuntu 20.04, aarch64 and x86_64) | No: EDU only |
| [unitree_sdk2_python](https://github.com/unitreerobotics/unitree_sdk2_python) | Python bindings (Python 3.8 or later, CycloneDDS 0.10.2) | No: EDU only |
| [unitree_ros2](https://github.com/unitreerobotics/unitree_ros2) | ROS 2 messages and examples: Foxy on Ubuntu 20.04, Humble on Ubuntu 22.04 ("recommend") | No: EDU only |

On an EDU, these tools talk to the robot over a wired Ethernet link; Unitree's [quick start](https://support.unitree.com/home/en/developer/Quick_start) sets the robot's computer at 192.168.123.161 and recommends Ubuntu 20.04 or 22.04. We list them so you know what the EDU docs assume, not because they work on our unit.

### Community tools for the Air and Pro

> [!CAUTION]
> These projects are **unofficial**: Unitree does not support them, and they work by speaking the same WebRTC protocol as the phone app. Firmware updates have broken them several times (for example, go2_ros2_sdk issues [#178](https://github.com/abizovnuralem/go2_ros2_sdk/issues/178), [#236](https://github.com/abizovnuralem/go2_ros2_sdk/issues/236) and [#238](https://github.com/abizovnuralem/go2_ros2_sdk/issues/238)). Since firmware 1.1.15 they need a **per-device key** that is fetched with the Unitree account's email and password. Only `[lab manager name]` fetches that key, and it never goes into a repo.

Checked on Sept. 30, 2026 with each repo's README and GitHub metadata:

| Project | What it does | License | Activity | Firmware noted in README | ROS 2 |
| --- | --- | --- | --- | --- | --- |
| [abizovnuralem/go2_ros2_sdk](https://github.com/abizovnuralem/go2_ros2_sdk) | Unofficial ROS 2 driver for the Go2 Air, Pro and EDU: joint states, IMU, lidar point cloud, camera, joystick, SLAM (slam_toolbox), Nav2, foxglove_bridge. WebRTC over Wi-Fi; CycloneDDS over Ethernet (EDU) | BSD-2-Clause | Last commit July 13, 2026; last release v0.2.0 (June 2024) | Notes behavior on v1.1.7; per-device AES-128 key from 1.1.15 | Tested on Ubuntu 22.04 with Humble, Iron and Rolling |
| [legion1581/unitree_webrtc_connect](https://github.com/legion1581/unitree_webrtc_connect) (was `go2_webrtc_connect`) | Python WebRTC driver for Go2 Air, Pro and EDU: local AP, local STA and remote (through Unitree's server, needs account credentials) | MIT | Release v2.2.0, Aug. 17, 2026 | 1.0.19-1.0.25, 1.1.1-1.1.14, 1.1.15 and later (with key) | None (a Python library, Python 3.8 or later) |
| [tfoldi/go2-webrtc](https://github.com/tfoldi/go2-webrtc) | The original WebRTC work the others build on | BSD-2-Clause | Last commit Jan. 19, 2026 (firmware 1.1.8 protocol); no releases | Not listed | None |

Of the distros go2_ros2_sdk lists, only Humble is still supported, until May 2027; Iron reached end of life on Dec. 4, 2024 ([ROS 2 distributions](https://docs.ros.org/en/rolling/Releases.html)). For the lab's ROS 2 setup, see [ROS 2](../tech-stack/ros2.md) and the lab-robots page in [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md).

Two rules for all of them:

- Close the Unitree Go app before you connect: go2_ros2_sdk says to "close the connection with a mobile app before connecting", and unitree_webrtc_connect raises `RobotBusyError` when another WebRTC client is connected.
- Pin the version you tested with, and write down the robot's firmware version next to it.

### Simulation

| Model or tool | What it gives you | Link |
| --- | --- | --- |
| MuJoCo Menagerie `unitree_go2` | MJCF model (BSD-3-Clause), MuJoCo 2.2.2 or later | [unitree_go2](https://github.com/google-deepmind/mujoco_menagerie/tree/main/unitree_go2) |
| unitree_mujoco | Unitree's MuJoCo simulator for SDK development; "only supports low-level development" | [unitree_mujoco](https://github.com/unitreerobotics/unitree_mujoco) |
| Isaac Lab | Go2 locomotion tasks `Isaac-Velocity-Rough-Unitree-Go2-v0` and `Isaac-Velocity-Flat-Unitree-Go2-v0` | [Isaac Lab environments](https://isaac-sim.github.io/IsaacLab/main/source/overview/environments.html) |
| unitree_rl_lab, unitree_rl_gym | Unitree's reinforcement-learning examples (Isaac Lab; Isaac Gym with MuJoCo sim-to-sim) | [unitree_rl_lab](https://github.com/unitreerobotics/unitree_rl_lab), [unitree_rl_gym](https://github.com/unitreerobotics/unitree_rl_gym) |
| unitree_ros `go2_description` | URDF and meshes (a ROS 1 and Gazebo package) | [go2_description](https://github.com/unitreerobotics/unitree_ros/tree/master/robots/go2_description) |

Controllers trained for low-level joint control run on the EDU through the SDK; there is no official route to deploy them on the Pro. Lab guides: [MuJoCo](../tech-stack/mujoco.md), [Isaac Sim](../tech-stack/isaac-sim.md), [Gazebo](../tech-stack/gazebo.md).

## Safety

Read the lab's safety rules first, especially [robots in motion](../lab-rules/safety.md#robots-in-motion) and [batteries](../lab-rules/safety.md#batteries). The rules below come from Unitree's official pages where noted; the rest are lab practice for any legged robot.

> [!WARNING]
> **Know how to stop it before you walk it.** Unitree's docs describe **damping mode** as "equivalent to a soft emergency stop": all joint motors stop and go limp, so the robot drops to the floor where it stands ([Motion Application](https://support.unitree.com/home/en/developer/Motion%20Application)). On the handheld remote it is <kbd>L2</kbd> + <kbd>B</kbd> ([official button map, PDF](https://oss-global-cdn.unitree.com/static/697b96893c144fea976e13815199bd70.pdf)). It is a software stop, not a hardware cutoff. How to trigger it from the app on our firmware: `[app emergency-stop steps, from training]`.

- **Clear the area.** Keep people, cables and bags out of its path. Unitree's [disclaimer](https://shop.unitree.com/pages/disclaimer) says not to use it in "densely populated areas" (people less than 1 m apart).
- **Use a spotter.** One person drives; a second person watches the robot and is ready to call for damping mode.
- **Plan for falls.** Walk it on flat, dry floor, away from stairs and table edges, until you have been trained on stairs and slopes. Unitree lists 5 °C to 35 °C and good weather as the operating range.
- **Tricks and fast gaits.** Unitree's motion docs flag flips and similar actions as "potentially dangerous" and say to keep a safe distance.
- **Minors.** Unitree's disclaimer says the Go2 is "not suitable for people under the age of 18". Ask `[director or lab manager]` before any demo with high school or middle school visitors.
- **Low battery.** After the low-battery warning, the robot crouches down by itself within 10 minutes ([About Go2](https://support.unitree.com/home/en/developer/about_Go2)). Stop before that.
- **Batteries.** Charge only with the Unitree charger for this battery (33.6 V, 3.5 A), on a non-flammable surface and never unattended. Unitree does not publish storage guidance on its own site; follow the lab's [battery rules](../lab-rules/safety.md#batteries).

> [!CAUTION]
> **Never pick up, carry or hang the robot while it is powered on.** Lie it down and power it off first. It weighs about 15 kg and its legs can move without warning. Unitree also says the Go2 must not be powered on while hanging.

## Troubleshooting

| Problem | What to try | Source |
| --- | --- | --- |
| The app or a community tool can't connect | Only one WebRTC client can connect at a time: close the app before using a community tool, and the other way round. The robot runs either AP mode or Wi-Fi (STA) mode, not both | [go2_ros2_sdk](https://github.com/abizovnuralem/go2_ros2_sdk), [unitree_webrtc_connect](https://github.com/legion1581/unitree_webrtc_connect), [network docs](https://support.unitree.com/home/en/developer/network%20service) |
| You need the robot's IP address for a community tool | In the app, open Device, then Data, then Automatic Machine Inspection, and look for "STA Network: wlan0" | [go2_ros2_sdk README](https://github.com/abizovnuralem/go2_ros2_sdk) |
| After a firmware update: "RSA key format is not supported", or the data channel never opens | Firmware 1.1.15 and later needs the per-device AES-128 key, passed in an environment variable (`ROBOT_AES_KEY`) set outside the repo. Ask `[lab manager name]`; check the project's issues for the current fix | [go2_ros2_sdk README](https://github.com/abizovnuralem/go2_ros2_sdk), [unitree_webrtc_connect README](https://github.com/legion1581/unitree_webrtc_connect) |
| Legs are in the wrong position after power-on | Power off, put the robot in its initial position on the floor and power on again. Never power on while it hangs | [Unitree FAQ](https://support.unitree.com/home/en/developer/FAQ) |
| Red status light | Slow flash: system abnormality or hardware failure. Fast flash: motor and IMU calibration failed. Power off and report it | [About Go2](https://support.unitree.com/home/en/developer/about_Go2) |
| Motor protection or a similar fault | Unitree says these faults "require a restart" | [Faults](https://support.unitree.com/home/en/developer/FAULTS) |
| The robot crouches down on its own | Low battery: swap or charge the battery | [About Go2](https://support.unitree.com/home/en/developer/about_Go2) |
| `unitree_sdk2` or `unitree_ros2` can't find the robot | Expected on the Pro: those tools need an EDU's wired interface | [Unitree FAQ](https://support.unitree.com/home/en/developer/FAQ) |

## Resources

- Official: [Go2 product page](https://www.unitree.com/go2/) · [developer docs](https://support.unitree.com/home/en/developer) · [About Go2](https://support.unitree.com/home/en/developer/about_Go2) · [FAQ](https://support.unitree.com/home/en/developer/FAQ) · [Go2 app](https://www.unitree.com/app/go2/) · [remote button map (PDF)](https://oss-global-cdn.unitree.com/static/697b96893c144fea976e13815199bd70.pdf) · [Unitree on GitHub](https://github.com/unitreerobotics)
- Community: [go2_ros2_sdk](https://github.com/abizovnuralem/go2_ros2_sdk) · [unitree_webrtc_connect](https://github.com/legion1581/unitree_webrtc_connect) · [go2-webrtc](https://github.com/tfoldi/go2-webrtc)
- Simulation: [MuJoCo Menagerie unitree_go2](https://github.com/google-deepmind/mujoco_menagerie/tree/main/unitree_go2) · [Isaac Lab environments](https://isaac-sim.github.io/IsaacLab/main/source/overview/environments.html)
- Lab: [ATR-Lab/go2_ws](https://github.com/ATR-Lab/go2_ws) · [lab robots and ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md)

## Related

- [Lab hardware index](README.md) and the [checklist before you use any hardware](README.md#before-you-use-any-hardware)
- [Booster K1](booster-k1.md), the lab's other legged robot
- [Lab safety rules](../lab-rules/safety.md)
- Tech stack: [ROS 2](../tech-stack/ros2.md) · [MuJoCo](../tech-stack/mujoco.md) · [Isaac Sim](../tech-stack/isaac-sim.md) · [Docker](../tech-stack/docker.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/hardware/unitree-go2.md)</sub>
