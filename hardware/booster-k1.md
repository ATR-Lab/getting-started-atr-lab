# Booster K1

> **Read this when** you are about to operate, program or check out the lab's Booster K1 humanoid robot.

This page covers the Booster K1 from Booster Robotics: its variants and specs, how to power it on and walk it, its software (SDK, ROS 2 interface and training tools) and its safety rules. The one thing to remember: the K1's emergency stop is **software only** (a soft stop that puts the joints in a limp, damped state), so a person must be ready to stop it every time it moves, and any code that drives the joints directly runs with the robot on a hoist.

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

The [Booster K1](https://www.booster.tech/booster-k1) is a humanoid robot (shaped roughly like a person) about 0.95 m tall with 22 degrees of freedom, made by [Booster Robotics](https://www.booster.tech/). It walks on two legs, has a depth camera and microphones in its head and runs Booster's locomotion controller on an onboard computer. You drive it with a game controller, the Booster App or your own code through Booster's SDK.

Booster sells three variants, **Geek**, **Education** and **Professional**, which differ mainly in onboard computer and battery (see [Key specs](#key-specs)). Our variant: `[K1 variant: Geek, Education or Professional]`.

What the lab uses it for: the K1 is the robot in the lab's [Expressive Motion](https://github.com/ATR-Lab/expressive-motion) project, and `[other current K1 projects and who leads them]`.

When you walk the K1 with the controller or the app, it is **teleoperated**: you steer, and Booster's locomotion controller keeps it balanced. When a trained policy or your own program drives it, it is autonomous or semi-autonomous. Label every demo and video with which one it is.

## Key specs

From Booster's [K1 product page](https://www.booster.tech/booster-k1) and the [K1 specifications page](https://docs.booster.tech/docs/product-manual/k1/getting-started/specifications/), checked Sept. 30, 2026. Where the two pages disagree, both values are shown.

| Spec | Geek | Education | Professional |
| --- | --- | --- | --- |
| Height, standing | About 0.95 m | About 0.95 m | About 0.95 m |
| Weight | About 19.5 kg | About 19.5 kg | About 19.5 kg |
| Degrees of freedom | 22: each leg 6, each arm 4, head 2 | Same | Same |
| Peak joint torque | 60 N·m | 60 N·m | 60 N·m |
| Onboard computer | ARM processor (model not named) | NVIDIA Jetson Orin NX 8GB | NVIDIA Jetson AGX Orin 32GB |
| AI compute (product page) | 48 TOPS (dense) | 117 TOPS | 200 TOPS |
| Memory and storage | 8 GB, 128 GB | 8 GB, 512 GB | 32 GB, 512 GB |
| Sensors | Stereo depth camera in the head; 9-axis IMU; circular three-microphone array; speaker | Same | Same |
| Battery | 2 Ah | 5 Ah | 5 Ah |
| Runtime | 30 min at 0.4 m/s (product page); 20 min at 1.1 m/s (specifications page) | 80 min at 0.4 m/s (product page); 1 h 10 min at 1.1 m/s (specifications page) | Same as Education |
| Charging time | 2 hours or less | 2 hours or less | 2 hours or less |
| Walking and turning speed | 1.1 m/s; 1.5 rad/s | Same | Same |
| Connectivity | Gigabit Ethernet, Wi-Fi 6, Bluetooth 5.2 | Same | Same |
| Operating environment | -10 °C to 45 °C; 5% to 90% humidity, no condensation | Same | Same |

Not published on the official pages we checked: battery voltage and watt-hours, camera and IMU models, payload and water or dust rating.

## In our lab

| Item | Details |
| --- | --- |
| Quantity | `[N]` |
| Variant | `[K1 variant: Geek, Education or Professional]` |
| Location | `[Room ###, shelf or cabinet]` |
| Owner or contact | `[K1 owner or contact name]` |
| Checkout | `[checkout procedure]` |
| Hoist or stand | `[where the lab's hoist or stand is, and who trains you on it]` |
| Firmware version | `[current firmware version, from /opt/booster/version.txt]` |
| Accounts and credentials | The Booster App needs a Booster account, and the robot has an SSH login. Ask `[lab manager name]`; never commit them to any repo |
| Lab repos | [ATR-Lab/expressive-motion](https://github.com/ATR-Lab/expressive-motion) (see below) |

**ATR-Lab/expressive-motion.** Its README describes a pipeline that turns a single video of a person walking into a Booster K1 reference motion and a training task for Booster's Isaac Lab tools (Booster Train, using BeyondMimic). It runs on x86_64 Linux with an NVIDIA GPU, pins Booster's `booster_train`, `booster_assets` and `booster_deploy` repos as submodules, and leaves training and deployment as manual steps: "Hardware execution additionally requires the upstream SDK, firmware, ROS 2, networking and safety procedures." Its code is MIT-licensed, but two dependencies (GVHMR and the SMPL body models) are for non-commercial research only.

## First steps

These steps follow Booster's [K1 quick start](https://docs.booster.tech/docs/product-manual/k1/getting-started/quick-start/). Do them with a trained lab member the first time.

> [!NOTE]
> Booster's docs say controller "button mappings vary by software version". Check our firmware version first ([check version](https://docs.booster.tech/docs/product-manual/k1/firmware-version/check-version/)) and use the mapping your trainer shows you if it differs from the list below.

1. Finish the [hardware checklist](README.md#before-you-use-any-hardware) and read [Safety](#safety) below.
2. Clear "an open, flat area of at least 2m × 2m" with no people or obstacles in it.
3. Install the battery with its indicator light facing up.
4. Press and hold the robot's power button for 3 seconds, and release it after the light turns on. Wait about one minute for the prompt sound, and **keep the robot still while you wait** so its IMU (motion sensor) can initialize.
5. Turn on the Booster controller: hold the Home button for 5 seconds. An Xbox controller also works; see the quick start.
6. Press <kbd>L2</kbd> + <kbd>Start</kbd> to enter PREP mode.
7. Press <kbd>L2</kbd> + <kbd>Up</kbd> to stand up. The robot then enters WALK mode on its own: the left stick moves it and the right stick turns it.
8. To finish: press <kbd>L2</kbd> + <kbd>Start</kbd> (PREP mode), lay the robot flat, then hold the power button for 3 seconds. Wait 6 seconds before you power it on again.

**The Booster App.** Download it from Booster's [app page](https://www.booster.tech/app-download), sign in with the lab's Booster account (ask `[lab manager name]`) and tap "Connect Robot" ([connect guide](https://docs.booster.tech/docs/product-manual/k1/basic-operations/connect-robot/)). Bluetooth and Location must be on. You can put the robot on the same Wi-Fi network as your phone, or connect your phone to the robot's own hotspot. The lab network is `[lab robot network]`.

**A wired connection from a computer.** Set your computer's Ethernet port to 192.168.10.10 with netmask 255.255.255.0, then log in:

```bash
# From a Linux or macOS terminal, over a direct Ethernet cable to the K1
ssh booster@192.168.10.102
```

Booster's connect guide publishes the factory-default password. Ask `[lab manager name]` for the lab's login instead, and never write it in a repo, notebook or chat.

**Firmware.** Check the installed version on the robot with `cat /opt/booster/version.txt`. The latest release listed on Sept. 30, 2026 was v1.8.0.9 (Sept. 15, 2026) ([version upgrade](https://docs.booster.tech/docs/product-manual/k1/firmware-version/software-upgrade/)). SDK and demo versions are tied to firmware versions, so don't upgrade without asking `[lab manager name]`.

### Modes

Booster's [modes page](https://docs.booster.tech/docs/product-manual/k1/basic-operations/modes/) defines five modes:

| Mode | What it does | Controller |
| --- | --- | --- |
| DAMP | Joints are damped: they resist being moved but don't move on their own. The docs call it "a safe mode" | <kbd>L2</kbd> + <kbd>Back</kbd> |
| PREP | Preparation mode; the robot must pass through PREP before WALK | <kbd>L2</kbd> + <kbd>Start</kbd> |
| WALK | Booster's locomotion controller walks and balances the robot | <kbd>R2</kbd> + <kbd>A</kbd> from PREP |
| CUSTOM | Your code controls every joint, legs included. Entered only from PREP or DAMP | From the SDK |
| PROTECT | Entered automatically after a fault such as exceeding limits or a fall; joints behave as in DAMP | Automatic |

"DAMP mode cannot switch directly to WALK mode; it must first enter PREP mode."

## Software

| Software | What it is | Notes |
| --- | --- | --- |
| Booster App | Phone app to connect, drive, run agents and upgrade firmware | [App page](https://www.booster.tech/app-download) |
| [Booster Studio](https://studio.booster.tech) | Booster's desktop tool for code editing, simulation, debugging and deployment | Virtual robots need Docker Desktop ([install guide](https://docs.booster.tech/docs/product-manual/booster-studio/quick-start/download-install/)); see [Docker](../tech-stack/docker.md) |
| [booster_robotics_sdk](https://github.com/BoosterRobotics/booster_robotics_sdk) | C++ SDK: headers plus a prebuilt library for aarch64 and x86_64. Supports K1, T1 and T2 | Apache-2.0 license text. README: Ubuntu 22.04; Booster's docs: Ubuntu 22.04 or 24.04. Uses Fast DDS |
| Python SDK | The SDK README installs `booster_robotics_sdk_python` with pip; Booster's docs describe a newer Python SDK, `boosteros` (Python 3.10 or later, firmware v1.7 or later) | [Python SDK overview](https://docs.booster.tech/docs/developer-guide/booster-os-python-sdk/sdk-overview/). Check which one matches our firmware |
| [booster_robotics_sdk_ros2](https://github.com/BoosterRobotics/booster_robotics_sdk_ros2) | ROS 2 package `booster_interface`: messages and services for robot control, with examples | The README names no ROS 2 distro and the repo has no license file yet. Booster's [booster_deploy guide](https://docs.booster.tech/docs/developer-guide/open-source/booster-deploy/) says ROS 2 Humble is already installed on the robot |

**What the SDK controls** ([C++ SDK overview](https://docs.booster.tech/docs/developer-guide/cpp/sdk-overview/)):

- **High-level services:** mode switching, omnidirectional walking, getting up, head rotation and similar calls. The walking itself stays Booster's controller.
- **Low-level topics:** real-time motor and IMU data, and joint commands. Joint commands "take effect only while the robot is in Custom mode" ([low-level topics](https://docs.booster.tech/docs/developer-guide/cpp/low-level-topics/)), which is when the hoist rule in [Safety](#safety) applies.

**ROS 2.** The on-robot ROS 2 install is Humble (supported until May 2027, per the [ROS 2 distributions page](https://docs.ros.org/en/rolling/Releases.html)). See [ROS 2](../tech-stack/ros2.md) and the lab-robots page in [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md).

### Training and simulation

| Repo or model | What it gives you | License |
| --- | --- | --- |
| [booster_train](https://github.com/BoosterRobotics/booster_train) | Reinforcement-learning tasks for T2, T1 and K1 in Isaac Lab (README: tested with Isaac Lab 2.3.2 and Isaac Sim 5.1.0) | Apache-2.0 text |
| [booster_deploy](https://github.com/BoosterRobotics/booster_deploy) | Runs the same policy in MuJoCo (sim-to-sim) and on the real robot (sim-to-real) | Apache-2.0 text |
| [booster_assets](https://github.com/BoosterRobotics/booster_assets) | K1 robot description: URDF (`robots/K1/K1_22dof.urdf`) and MuJoCo XML (`robots/K1/K1_22dof.xml`) | BSD-3-Clause |
| [booster_gym](https://github.com/BoosterRobotics/booster_gym) | Older Isaac Gym framework; **T1 only**. Booster's docs point K1 users to booster_train and booster_deploy | Apache-2.0 text |
| [robocup_demo](https://github.com/BoosterRobotics/robocup_demo) | Booster's soccer demo (vision, decision-making, game controller) for the K1 | Apache-2.0 |

MuJoCo Menagerie and the Isaac Sim asset library include Booster's **T1**, not the K1; for the K1, use the models in booster_assets. Lab guides: [Isaac Sim](../tech-stack/isaac-sim.md), [MuJoCo](../tech-stack/mujoco.md).

## Safety

Read the lab's safety rules first, especially [robots in motion](../lab-rules/safety.md#robots-in-motion) and [batteries](../lab-rules/safety.md#batteries). Quotes below are from Booster's [K1 safety page](https://docs.booster.tech/docs/product-manual/k1/getting-started/safety-warnings/) unless another source is linked.

> [!WARNING]
> **The emergency stop is software only.** Booster's [overview](https://docs.booster.tech/docs/product-manual/k1/getting-started/overview/) says "the joystick, App, and back-panel buttons can all trigger a soft emergency stop", which switches the joints to a damped state. The docs don't describe a hardware emergency-stop button. Keep the controller in your hand whenever the robot is powered on, and know the DAMP command (<kbd>L2</kbd> + <kbd>Back</kbd> in the current docs; confirm it for our firmware: `[DAMP command on our firmware]`). In DAMP the robot stops holding itself up, so expect it to fall.

- **Clear the area.** Make sure "there are no people or obstacles within the robot's operating range". Keep people away during full-body actions such as dances.
- **Use a spotter.** One person drives; a second person watches the robot and is ready to stop it.
- **Plan for falls.** The robot is about 19.5 kg. Booster warns that "Carpet has high resistance and can increase the risk of falling"; large full-body actions belong on hard floors such as rubber, cement or tile.
- **Always PREP before WALK**, with the robot "standing securely on the ground".
- **Upgrades.** Installing software stops the motion controller and the joints "no longer output torque". Lay the robot flat, switch to DAMP and keep the power on until the upgrade finishes.
- **Batteries.** Charge with the Booster charger: the charger light is red while charging and green when full ([charging](https://docs.booster.tech/docs/product-manual/k1/basic-operations/charging/)). Booster's [service terms](https://www.booster.tech/service) exclude damage from non-original battery packs. Booster's public docs give no storage guidance; follow the lab's [battery rules](../lab-rules/safety.md#batteries).
- **Minors.** Ask `[director or lab manager]` before any demo with high school or middle school visitors.

> [!CAUTION]
> **Do not lift the robot while it walks.** The quick start warns that in WALK mode "it may fail to detect the ground and kick unpredictably, causing injury". Put it in PREP and lay it flat, or power it off, before you pick it up. During motion, "do not touch any part of the robot with your body except the handle."

### Running your own code

> [!CAUTION]
> **Running your own joint-level code (CUSTOM mode):** "all joints, including the legs, are controlled by your code, and the robot can easily lose balance and fall." Booster says to "use a hoist to protect the robot throughout the process" and to validate the code in simulation first.

## Troubleshooting

| Problem | What to try | Source |
| --- | --- | --- |
| Buttons don't do what the docs say | Mappings vary by software version: check the firmware version and the matching manual | [Joystick control](https://docs.booster.tech/docs/product-manual/k1/basic-operations/joystick-control/) |
| The robot won't walk from DAMP | DAMP can't switch straight to WALK: go to PREP first | [Modes](https://docs.booster.tech/docs/product-manual/k1/basic-operations/modes/) |
| The robot went limp on its own | It entered PROTECT mode after a fault such as exceeding limits or falling. Support it, then restart from PREP | [Modes](https://docs.booster.tech/docs/product-manual/k1/basic-operations/modes/) |
| The Python SDK fails with `LocoClientInitError` | The robot needs "typically 30–60 seconds after boot" before the SDK can connect | [Python SDK FAQ](https://docs.booster.tech/docs/developer-guide/booster-os-python-sdk/faq-and-debugging-tools/faq/) |
| Your first walking commands are too fast | Booster recommends starting velocity commands at 0.1 | [Python SDK FAQ](https://docs.booster.tech/docs/developer-guide/booster-os-python-sdk/faq-and-debugging-tools/faq/) |
| Booster support asks for logs | Upload from the app, or use `booster-cli log` on the robot. The robot's clock defaults to UTC+8, so convert your time range | [Log retrieval](https://docs.booster.tech/docs/product-manual/k1/troubleshooting/logs/) |
| The software is badly broken | Booster documents a factory reset; "do not cut off power during the recovery process". Ask `[lab manager name]` before you run it | [Restore factory settings](https://docs.booster.tech/docs/product-manual/k1/troubleshooting/restore-factory-settings/) |

Booster's remote support uses a third-party remote-desktop tool. Check with `[lab manager name]` before you install it on a lab machine.

## Resources

- Official: [K1 product page](https://www.booster.tech/booster-k1) · [Booster docs](https://docs.booster.tech/) · [K1 quick start](https://docs.booster.tech/docs/product-manual/k1/getting-started/quick-start/) · [K1 safety](https://docs.booster.tech/docs/product-manual/k1/getting-started/safety-warnings/) · [open-source page](https://www.booster.tech/open-source) · [Booster Robotics on GitHub](https://github.com/BoosterRobotics) · [service terms](https://www.booster.tech/service)
- Booster does not link a public forum or Discord from its site; for support, see the contact options on the [service page](https://www.booster.tech/service).
- Lab: [ATR-Lab/expressive-motion](https://github.com/ATR-Lab/expressive-motion) · [lab robots and ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md)

## Related

- [Lab hardware index](README.md) and the [checklist before you use any hardware](README.md#before-you-use-any-hardware)
- [Unitree Go2 Pro](unitree-go2.md), the lab's other legged robot
- [Lab safety rules](../lab-rules/safety.md)
- Tech stack: [Isaac Sim](../tech-stack/isaac-sim.md) · [MuJoCo](../tech-stack/mujoco.md) · [ROS 2](../tech-stack/ros2.md) · [Docker](../tech-stack/docker.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/hardware/booster-k1.md)</sub>
