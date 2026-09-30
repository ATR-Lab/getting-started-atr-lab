# Yahboom ROSMASTER X3

> **Read this when** you are about to drive, program or check out the lab's Yahboom ROSMASTER X3 mobile robot, or run SLAM and navigation on it.

This page covers the ROSMASTER X3, a small mecanum-wheel robot for learning ROS: its hardware, which controller and ROS version it runs, how to power it on and connect, its lithium battery rules and common fixes. The one thing to remember: **which ROS 2 version you get depends on the main controller**. Yahboom ships ROS 2 Humble on its Jetson Orin controllers but ROS 2 Foxy (in Docker) on the Raspberry Pi 5 and Jetson Nano, and Foxy is past end of life.

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

The [ROSMASTER X3](https://category.yahboom.net/products/rosmaster-x3) from Yahboom is a four-wheel mobile robot with mecanum wheels (wheels with angled rollers, so it can drive sideways and turn in place), an aluminum chassis, a lidar, a depth camera and an STM32-based expansion board that drives the motors and reads the IMU. A main controller (a Jetson or a Raspberry Pi 5) runs Linux and ROS on top. Yahboom's [tutorials](http://www.yahboom.net/study/ROSMASTER-X3) cover driving, SLAM mapping, navigation, vision and voice.

Our unit's main controller: `[main controller]`. What the lab uses it for: `[current ROSMASTER X3 projects and who leads them]`.

Driving it with the gamepad or the phone app is **teleoperation**. When it follows a Nav2 plan or explores a map by itself, it is **autonomous**. Label every demo and video with which one it is.

## Key specs

From the [product page](https://category.yahboom.net/products/rosmaster-x3) and the spec images on it, checked Sept. 30, 2026. Many of Yahboom's specs appear only in images, and some differ between purchase options.

| Spec | ROSMASTER X3 |
| --- | --- |
| Drive | Four mecanum wheels (65 mm), omnidirectional; pendulum suspension |
| Motors | Four 520 metal gear motors with encoders |
| Body | Anodized aluminum alloy |
| Size | About 300 mm long (238 mm chassis) and 199 mm wide |
| Weight | 3.2-4.6 kg, depending on options |
| Battery | 12.6 V, 6,000 mAh, 2C lithium pack, with charger |
| Runtime | About 1.5 hours (Raspberry Pi 5 or Jetson Nano); about 1 hour (Jetson Orin Nano Super or Orin NX Super) |
| Lidar | SLAM A1 (0.15-12 m) or S2L (0.05-18 m), depending on the kit |
| Depth camera | Orbbec Astra Pro Plus (0.6-8 m) |
| Expansion board | STM32F103RCT6 microcontroller, ICM20948 nine-axis IMU, four motor drivers, 12 V input |
| Other outputs | RGB taillight, buzzer, OLED display, servo interfaces |
| Networking | Wi-Fi (LAN or hotspot mode) |
| Control | Phone app (iOS and Android), PC, gamepad |
| Protection | Short-circuit and overcurrent protection |

Yahboom's Q&A answers give a top speed of 1.0 m/s; no spec table lists it, and no payload is published.

### Main controller options

| Main controller | Operating system and ROS as shipped | Boot media shipped |
| --- | --- | --- |
| Raspberry Pi 5 (8 GB) | Raspberry Pi OS; ROS 1 Melodic or ROS 2 Foxy in Docker | 64 GB microSD card |
| Jetson Nano 4GB | Ubuntu 18.04; ROS 1 Melodic, or ROS 2 Foxy in Docker | 64 GB USB drive |
| Jetson Orin Nano Super (4 GB or 8 GB) | Ubuntu 22.04 with ROS 2 Humble (JetPack 6.2 image) | 256 GB SSD |
| Jetson Orin NX Super (8 GB or 16 GB) | Ubuntu 22.04 with ROS 2 Humble (JetPack 6.2 image) | 256 GB SSD |

Kits come in Standard, Advanced, Superior and Ultimate tiers, with or without the main controller; higher tiers add a voice module, a 7-inch screen and the S2L lidar.

## In our lab

| Item | Details |
| --- | --- |
| Quantity | `[N]` |
| Main controller | `[main controller]` |
| Kit tier and lidar | `[Standard, Advanced, Superior or Ultimate; A1 or S2L lidar]` |
| Location | `[Room ###, shelf or cabinet]` |
| Owner or contact | `[ROSMASTER X3 owner or contact name]` |
| Checkout | `[checkout procedure]` |
| Accounts and credentials | Yahboom's tutorials publish the factory usernames and passwords for the controller, Jupyter Lab, VNC and the robot's hotspot. Ask `[lab manager name]` for the lab's changed logins; never commit them to any repo |
| Lab repos | `[lab ROSMASTER X3 repo, if any]` |

The lab's public [ATR-Lab/yahboom_r2l_ros2](https://github.com/ATR-Lab/yahboom_r2l_ros2) repo is for a **different Yahboom robot, the R2L** (a ROS 2 Humble port from ROS 1 Noetic). It is not an X3 driver, but its structure is a useful example of a Yahboom ROS 2 workspace.

## First steps

These steps follow Yahboom's [ROSMASTER X3 tutorials](http://www.yahboom.net/study/ROSMASTER-X3). Do them with a trained lab member the first time.

1. Finish the [hardware checklist](README.md#before-you-use-any-hardware) and read [Safety](#safety) below.
2. **Assembly.** The robot ships unassembled ([unboxing post](https://category.yahboom.net/blogs/news/unboxing-rosmaster-x3)); the study page has assembly videos. Ours is `[assembled or not]`.
3. **Charge the battery** with the Yahboom charger, main power switch off.
4. **Power on with the robot flat on the floor.** It calibrates its IMU at power-on, so "it should be placed horizontally on the ground" until it beeps ([battery and usage precautions](https://www.yahboom.net/public/upload/upload-html/1743656067/2.%20Precautions%20for%20battery.html)).
5. **Connect.** Out of the box the controller makes a Wi-Fi hotspot and shows its IP address on the OLED screen. Connect your laptop or phone to it, or switch the robot to the lab network (`[lab robot network]`) ([static IP and hotspot mode](https://www.yahboom.net/public/upload/upload-html/1686909289/5.%20Static%20IP%20and%20hotspot%20mode.html)). Then use SSH, VNC or Jupyter Lab on port 8888 ([remote control](https://www.yahboom.net/public/upload/upload-html/1743494533/3.%20Remote%20control.html)).
6. **Change the default passwords** if `[lab manager name]` hasn't already. They are published online.
7. **Set the robot type and lidar model** once, from the robot's terminal, using the script for your lidar (A1 or S2) ([first trial](https://www.yahboom.net/public/upload/upload-html/1712911734/First%20Trial.html)):

   ```bash
   # On the robot, for an X3 with the A1 lidar
   sh ~/Rosmaster/RobotType/set_X3_A1.sh
   # Or, for the S2L lidar
   sh ~/Rosmaster/RobotType/set_X3_S2.sh
   ```

   Close and reopen the terminal; it should print the robot model.

8. **Drive it** with the gamepad (press <kbd>R2</kbd> to release the motion lock) or the **MakerControl** phone app ([app tutorial](https://www.yahboom.net/public/upload/upload-html/1729155906/1.%20Mobile%20APP%20remote%20control%20tutorial.html)).
9. **Before you run your own ROS programs,** stop the factory "large program" that starts at boot; otherwise the two fight over the hardware ([turn off the startup process](https://www.yahboom.net/public/upload/upload-html/1713174096/2.Turn%20off%20the%20self-starting%20process%20at%20startup.html)).
10. **When you finish,** switch off the main power switch on the expansion board.

## Software

| Software | What it is | Where |
| --- | --- | --- |
| System images | Pre-built images per controller (ROS 1 and ROS 2), already on the shipped microSD card, USB drive or SSD; replacements download from the study page | [Study page](http://www.yahboom.net/study/ROSMASTER-X3) |
| ROS 2 Docker image | ROS 2 Foxy for the Raspberry Pi 5 and Jetson Nano, updated with `docker pull` | Yahboom tutorials |
| Tutorial source code | Linked as "Code" from the study page (a cloud-drive folder, not GitHub) | [Study page](http://www.yahboom.net/study/ROSMASTER-X3) |
| Tutorial PDFs | Yahboom's GitHub repo holds the tutorial documents | [YahboomTechnology/ROSMASTERX3](https://github.com/YahboomTechnology/ROSMASTERX3) |
| MakerControl | Phone app for driving | [App tutorial](https://www.yahboom.net/public/upload/upload-html/1729155906/1.%20Mobile%20APP%20remote%20control%20tutorial.html) |
| Rosmaster_Lib | Python driver library for the expansion board, preinstalled on the images | Yahboom tutorials |

The tutorials cover ROS 2 mapping with Gmapping and Cartographer, RTAB-Map 3D mapping, Nav2 navigation and obstacle avoidance, vision, voice control and YOLO object recognition (on the Orin Super images).

**ROS 2 versions.** ROS 2 Humble (on the Orin controllers) is supported until May 2027. ROS 2 Foxy (on the Pi 5 and Nano images) reached end of life on June 20, 2023 ([ROS 2 distributions](https://docs.ros.org/en/rolling/Releases.html)): it gets no security fixes, and current ROS 2 tutorials won't match it. If our unit runs Foxy, talk to `[lab manager name]` before you build a project on it. Lab guides: [ROS 2](../tech-stack/ros2.md), [Docker](../tech-stack/docker.md), [Gazebo](../tech-stack/gazebo.md) and the lab-robots page in [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md).

**Firmware.** Yahboom says of the expansion board's firmware: "If it is not necessary, please do not update the firmware" ([firmware update](https://www.yahboom.net/public/upload/upload-html/1743494450/1.%20Update%20the%20firmware.html)).

## Safety

Read the lab's safety rules first, especially [robots in motion](../lab-rules/safety.md#robots-in-motion) and [batteries](../lab-rules/safety.md#batteries). Battery rules below are quoted or summarized from Yahboom's [battery and usage precautions](https://www.yahboom.net/public/upload/upload-html/1743656067/2.%20Precautions%20for%20battery.html).

> [!WARNING]
> **Lithium battery.** "It is strictly forbidden to use batteries or chargers not provided by the company." Turn the main power switch off before charging, don't use the robot while it charges and "Someone needs to be present when charging." Unplug the charger when its light turns from red to green. If the pack or charger swells, gets very hot or smells, stop using it and tell `[lab safety contact]`. If it smokes or catches fire, follow the lab's [battery emergency rule](../lab-rules/safety.md#batteries): leave the room, pull the fire alarm and call 911. (Yahboom mentions sand or a dry-powder extinguisher; use one only if you are trained to.)

- **Low battery.** Below 9.6 V the expansion board beeps and the MCU light flashes fast: switch off and charge.
- **Storage.** For long storage, keep the pack at 11.1-11.7 V, remove it from the robot and store it away from metal objects, with its insulating wrap intact, in `[battery storage location]`.
- **Temperature and water.** Use it between 0 °C and 35 °C, and never in damp conditions or rain.
- **Lidar.** It spins as soon as the robot powers on: "do not block the rotation of the lidar".
- **Load.** Yahboom forbids loads beyond the product's capacity but publishes no payload number, so don't add weight without asking `[lab manager name]`.
- **Autonomous runs.** Stay within reach of the power switch or the gamepad, and keep people out of its path.

> [!CAUTION]
> **It can move in any direction without turning first.** Mecanum wheels let the robot slide sideways, so clear the floor around it, not just in front. Keep it off tables, and keep feet and fingers away from the wheels while it runs.

## Troubleshooting

| Problem | What to try | Source |
| --- | --- | --- |
| The MCU light stays on or off (it should flash twice every three seconds) | Press the RESET button on the expansion board, with the robot flat on the floor | [Battery and usage precautions](https://www.yahboom.net/public/upload/upload-html/1743656067/2.%20Precautions%20for%20battery.html) |
| The gamepad does nothing | Plug its receiver into the outermost USB port on the hub, check the mode (PC/PCS for Jetson controllers, X-BOX for Raspberry Pi) and press <kbd>R2</kbd> to release the motion lock | [Gamepad tutorial](https://www.yahboom.net/public/upload/upload-html/1745735032/3.%20USB%20wireless%20handle%20%2B%20mobile%20phone%20screen%20remote%20control%20tutorial.md.html) |
| Your ROS program behaves oddly or can't open the hardware | The factory program is still running: stop it first | [Turn off the startup process](https://www.yahboom.net/public/upload/upload-html/1713174096/2.Turn%20off%20the%20self-starting%20process%20at%20startup.html) |
| No windows (GUI) from inside the Docker container (Raspberry Pi) | Follow the container tutorial's fixes, including the camera device path, which can change after re-plugging | [Enter the robot's Docker container](https://www.yahboom.net/public/upload/upload-html/1687333441/5%E3%80%81Enter%20the%20bot%27s%20docker%20container.html) |
| A replacement Jetson won't start the robot software | The Jetson's JetPack version must match Yahboom's image | [Using your own Jetson board](https://www.yahboom.net/public/upload/upload-html/1730340830/Using%20your%20own%20Jetson%20board%2C%20ROSMASTER%20X3%20cannot%20start%20normally.html) |
| You can't find the robot on the network | Read the IP address from the OLED screen; check whether it is in hotspot or LAN mode | [Remote control](https://www.yahboom.net/public/upload/upload-html/1743494533/3.%20Remote%20control.html) |

## Resources

- Official: [ROSMASTER X3 product page](https://category.yahboom.net/products/rosmaster-x3) · [ROSMASTER X3 tutorials (study page)](http://www.yahboom.net/study/ROSMASTER-X3) · [YahboomTechnology/ROSMASTERX3](https://github.com/YahboomTechnology/ROSMASTERX3) · [expansion board V3.0](https://www.yahboom.net/public/upload/upload-html/1713173945/1.About%20expansion%20boardV3.0.html) · [Orin Nano Super update](https://category.yahboom.net/blogs/news/rosmaster-x3-update-jetson-orin-nano-super)
- Lab: [ATR-Lab/yahboom_r2l_ros2](https://github.com/ATR-Lab/yahboom_r2l_ros2) (R2L, not X3) · [lab robots and ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md)

## Related

- [Lab hardware index](README.md) and the [checklist before you use any hardware](README.md#before-you-use-any-hardware)
- [Raspberry Pi 5](raspberry-pi-5.md), one of the X3's controller options
- [Lab safety rules](../lab-rules/safety.md)
- Tech stack: [ROS 2](../tech-stack/ros2.md) · [Docker](../tech-stack/docker.md) · [Gazebo](../tech-stack/gazebo.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/hardware/rosmaster-x3.md)</sub>
