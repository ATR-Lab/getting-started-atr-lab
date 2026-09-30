# ROBOTIS OpenManipulator-X

> **Read this when** you are about to set up, program or check out the lab's OpenManipulator-X robot arm.

This page covers the ROBOTIS OpenManipulator-X: its specs, how to wire and power it, how to run it with ROS 2 Jazzy (or Humble), MoveIt 2 and Gazebo, how to configure its servos with DYNAMIXEL Wizard 2.0 and its safety rules. The one thing to remember: **set the arm's starting pose by hand with torque off, then launch**. Launching turns torque on and locks every joint, and the arm won't move if any joint starts outside its range.

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

The [OpenManipulator-X](https://docs.robotis.com/docs/systems/openmanipulator_x/overview/) (ROBOTIS model RM-X52-TNM) is a small desktop robot arm with four joints and a gripper, built from five DYNAMIXEL XM430-W350-T smart servos. A computer drives it through a USB interface (the ROBOTIS U2D2 or an OpenCR board), using ROS 2, the DYNAMIXEL SDK or Arduino.

What the lab uses it for: `[current OpenManipulator-X projects and who leads them]`.

Driving it joint by joint from the keyboard or the GUI is **teleoperation**; when MoveIt 2 or your code plans and executes a motion, the arm moves autonomously along that plan. Label demos and videos with which one it is.

> [!NOTE]
> ROBOTIS has moved its e-Manual (emanual.robotis.com) into **ROBOTIS Docs** (docs.robotis.com), and the old pages carry a banner saying the e-Manual website "will be removed in July". This page links to ROBOTIS Docs.

## Key specs

From the [ROBOTIS Docs specification page](https://docs.robotis.com/docs/systems/openmanipulator_x/specification/), checked Sept. 30, 2026.

| Spec | Value |
| --- | --- |
| Model | RM-X52-TNM |
| Degrees of freedom | 5: four arm joints plus a one-DOF gripper |
| Actuators | DYNAMIXEL XM430-W350-T (five) |
| Payload | 500 g |
| Reach | 380 mm |
| Repeatability | Under 0.2 mm |
| Joint speed | 46 rpm |
| Weight | 0.70 kg |
| Gripper stroke | 20-75 mm |
| Input voltage | 12 V |
| Communication | TTL multidrop bus, DYNAMIXEL Protocol 2.0, 1 Mbps by default |
| Default servo IDs | 11, 12, 13, 14 (joints 1-4); 15 (gripper) |
| Software | ROS, DYNAMIXEL SDK, Arduino, Processing |
| Main controller | PC or OpenCR |

The XM430-W350-T servo takes 10.0-14.8 V, 12.0 V recommended ([XM430-W350 reference](https://docs.robotis.com/docs/dxl/model_reference/x_series/xm_series/xm430-w350)). ROBOTIS recommends its SMPS 12V 5A PS-10 power supply ([quick start](https://docs.robotis.com/docs/systems/openmanipulator_x/quick_start_guide/)); the arm is sold without a power supply or controller.

## In our lab

| Item | Details |
| --- | --- |
| Quantity | `[N]` |
| Location | `[Room ###, bench or shelf]` |
| Owner or contact | `[OpenManipulator-X owner or contact name]` |
| Checkout | `[checkout procedure]` |
| Interface and power supply | `[U2D2 with U2D2 Power Hub Board, or OpenCR; which 12 V supply]` |
| Lab computer set up for it | `[computer name or "bring your own Ubuntu 24.04 laptop"]` |
| Accounts and credentials | None needed for the arm itself. Lab computer logins: ask `[lab manager name]`; never commit them |
| Lab repos | [ATR-Lab/multi-servo-dynamixel-library](https://github.com/ATR-Lab/multi-servo-dynamixel-library) (older, see below) |

**ATR-Lab/multi-servo-dynamixel-library** holds older lab code for driving several DYNAMIXEL servos: Python driver helpers and a ROS 1 (catkin) workspace, last updated in November 2021. Its README has only a title, it is not ROS 2 and it was not written for the OpenManipulator-X. Treat it as reference, not as the arm's driver.

## First steps

These steps follow the ROBOTIS [quick start](https://docs.robotis.com/docs/systems/openmanipulator_x/quick_start_guide/) and [basic operation](https://docs.robotis.com/docs/systems/openmanipulator_x/quick_start_guide/basic_operation) pages for **ROS 2 Jazzy on Ubuntu 24.04**. For Humble on Ubuntu 22.04, see [Software](#software).

1. Finish the [hardware checklist](README.md#before-you-use-any-hardware) and read [Safety](#safety) below.
2. **Wire it with the power off.** With the U2D2 (the option ROBOTIS recommends): micro USB from the U2D2 to the computer, the arm's DYNAMIXEL cable to the U2D2 and 12 V power to the U2D2 Power Hub Board. Check the polarity of the power terminal before you switch on.
3. **Switch on the power** and check that every DYNAMIXEL LED blinks once.
4. **Install the software** (next section), either in the ROBOTIS Docker container or directly on Ubuntu.
5. **Set the starting pose.** With torque off, move each joint by hand to the start pose shown on the [basic operation](https://docs.robotis.com/docs/systems/openmanipulator_x/quick_start_guide/basic_operation) page. "Please check each joint position before running OpenMANIPULATOR-X."
6. **Launch the arm** and drive it from the keyboard (below).
7. **When you finish,** move the arm to a resting pose and support it before you stop the launch or switch off the power: without torque, the joints can't hold the arm up.

### Install: Docker (ROBOTIS recommends this for Jazzy)

"For ROS 2 Jazzy, we recommend using Docker for a more reliable and isolated development environment." The container already sets the USB latency timer. Lab guide: [Docker](../tech-stack/docker.md).

```bash
# Ubuntu 24.04 host with Docker installed
git clone -b jazzy https://github.com/ROBOTIS-GIT/open_manipulator.git
cd open_manipulator
./docker/container.sh start
./docker/container.sh enter
```

`./docker/container.sh stop` removes the container; only files in `/workspace` are kept.

### Install: directly on Ubuntu 24.04 with ROS 2 Jazzy

```bash
# Let your user open USB serial ports; log out and back in afterward
sudo usermod -aG dialout $USER

mkdir -p ~/ros2_ws/src
cd ~/ros2_ws/src
git clone -b jazzy https://github.com/ROBOTIS-GIT/DynamixelSDK.git
git clone -b jazzy https://github.com/ROBOTIS-GIT/dynamixel_interfaces.git
git clone -b jazzy https://github.com/ROBOTIS-GIT/dynamixel_hardware_interface.git
git clone -b jazzy https://github.com/ROBOTIS-GIT/open_manipulator.git

cd ~/ros2_ws
# rosdep init is needed once per machine; skip it if it says rosdep is already initialized
sudo rosdep init
rosdep update
rosdep install --from-paths src -y --ignore-src
colcon build --symlink-install --cmake-args -DCMAKE_BUILD_TYPE=Release
source ~/ros2_ws/install/setup.bash

# Install the udev rule that lowers the USB latency timer from 16 ms to 1 ms
ros2 run open_manipulator_bringup om_create_udev_rules
```

Check the latency timer (it should read 1 after the rule is installed and the U2D2 is reconnected):

```bash
cat /sys/bus/usb-serial/devices/ttyUSB0/latency_timer
```

### Run the arm

```bash
# Terminal 1: start the arm through the U2D2 (joints lock with torque on)
ros2 launch open_manipulator_bringup open_manipulator_x.launch.py

# Through an OpenCR board instead of the U2D2
ros2 launch open_manipulator_bringup open_manipulator_x.launch.py port_name:=/dev/ttyACM0
```

```bash
# Terminal 2: keyboard teleoperation
ros2 run open_manipulator_teleop open_manipulator_x_teleop
```

The teleop keys: <kbd>1</kbd>/<kbd>q</kbd>, <kbd>2</kbd>/<kbd>w</kbd>, <kbd>3</kbd>/<kbd>e</kbd>, <kbd>4</kbd>/<kbd>r</kbd> move joints 1-4, and <kbd>o</kbd>/<kbd>p</kbd> move the gripper ([ROS operation](https://docs.robotis.com/docs/systems/openmanipulator_x/ros/ros_operation)).

## Software

### ROS 2 support

| Distro | Ubuntu | Branch | Notes |
| --- | --- | --- | --- |
| ROS 2 Jazzy | 24.04 | `jazzy` | Newest documented; Docker recommended. Packages: `open_manipulator_bringup`, `open_manipulator_moveit_config`, `open_manipulator_gui`, `open_manipulator_teleop` |
| ROS 2 Humble | 22.04 | `humble` | Package names start with `open_manipulator_x_` (for example `open_manipulator_x_bringup`) |
| ROS 1 Noetic | 20.04 | `noetic` | Still documented; the branch's last commit is from July 2021 |

The code is in [ROBOTIS-GIT/open_manipulator](https://github.com/ROBOTIS-GIT/open_manipulator) (Apache-2.0; release 5.1.3 on Sept. 28, 2026). Jazzy is supported until May 2029 and Humble until May 2027 ([ROS 2 distributions](https://docs.ros.org/en/rolling/Releases.html)). Lab guides: [ROS 2](../tech-stack/ros2.md) and the lab-robots page in [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md).

<details>
<summary>Humble launch commands (Ubuntu 22.04)</summary>

From the Humble tabs of the same ROBOTIS pages:

```bash
ros2 run open_manipulator_x_bringup create_udev_rules
ros2 launch open_manipulator_x_bringup hardware.launch.py
ros2 launch open_manipulator_x_bringup gazebo.launch.py
ros2 launch open_manipulator_x_moveit_config moveit_core.launch.py
ros2 launch open_manipulator_x_gui open_manipulator_x_gui.launch.py
```

Keyboard teleoperation on Humble runs `ros2 launch open_manipulator_x_moveit_config servo.launch.py` first, then `ros2 run open_manipulator_x_teleop open_manipulator_x_teleop`.

</details>

### MoveIt 2, GUI and Gazebo (Jazzy)

```bash
# MoveIt 2 on the real arm: run bringup first, then in a second terminal
ros2 launch open_manipulator_moveit_config open_manipulator_x_moveit.launch.py

# GUI: with bringup and MoveIt 2 running, in a third terminal
ros2 launch open_manipulator_gui open_manipulator_x_gui.launch.py
```

```bash
# Gazebo simulation, then MoveIt 2 against the simulated arm
ros2 launch open_manipulator_bringup open_manipulator_x_gazebo.launch.py
ros2 launch open_manipulator_moveit_config open_manipulator_x_moveit.launch.py use_sim:=true
```

Sources: [ROS simulation](https://docs.robotis.com/docs/systems/openmanipulator_x/ros/ros_simulation), [ROS controller experiment](https://docs.robotis.com/docs/systems/openmanipulator_x/ros_controller/ros_controller_experiment). ROBOTIS notes that gravity compensation "is not supported yet". Lab guide: [Gazebo](../tech-stack/gazebo.md).

### DYNAMIXEL Wizard 2.0

[DYNAMIXEL Wizard 2.0](https://docs.robotis.com/docs/software/dynamixel_wizard_2_0/introduction) is ROBOTIS's desktop tool for finding, testing and configuring DYNAMIXEL servos, including firmware updates and recovery. It runs on Windows 10 and 11, Ubuntu 22.04 and 24.04 and macOS 13 or later; download it from that page.

Typical uses ([basic features](https://docs.robotis.com/docs/software/dynamixel_wizard_2_0/basic_features)):

- **Scan** (Device, then Scan) for Protocol 2.0 at 1 Mbps, IDs 11-15, to check that all five servos answer.
- **Change an ID or baud rate.** These live in the servo's EEPROM, which "can only be written to if Torque Enable(64) is cleared" (torque off).
- **Firmware recovery** (Tools, then Firmware Recovery), with "only one DYNAMIXEL" connected to the port.
- The gripper (ID 15) "requires Current based Position Control Mode"; don't change its operating mode.

Close the Wizard before you launch ROS 2: only one program can hold the serial port.

### Simulation models

- **MuJoCo:** DeepMind's MuJoCo Menagerie has no OpenManipulator-X model. ROBOTIS publishes one in [robotis_mujoco_menagerie](https://github.com/ROBOTIS-GIT/robotis_mujoco_menagerie) (`robotis_open_manipulator_x/`), and the `jazzy` branch of open_manipulator includes MJCF files under `open_manipulator_description/mujoco/`. Lab guide: [MuJoCo](../tech-stack/mujoco.md).
- **Gazebo:** the launch files above.

## Safety

Read the lab's safety rules first, especially [robots in motion](../lab-rules/safety.md#robots-in-motion).

> [!WARNING]
> **Keep hands out of the workspace while torque is on.** The XM430 servo reference says: "Never place fingers, arms, toes, and other body parts near product during operation." The arm reaches 380 mm in every direction around its base, and the gripper and folding joints are pinch points. Clear that space of people, cables and loose objects before you launch.

- **Check the pose first.** Launching locks every joint with torque on, and "the manipulator will not operate if any joint is out of operable range."
- **Power.** Use a 12 V supply (ROBOTIS recommends its SMPS 12V 5A). Check the polarity of the power terminal before energizing it, and "do not connect or disconnect DYNAMIXEL cables while power is being supplied" ([XM430-W350 reference](https://docs.robotis.com/docs/dxl/model_reference/x_series/xm_series/xm430-w350)).
- **Stay within payload.** 500 g, including anything the gripper holds.
- **Test new motions in simulation** (Gazebo or MuJoCo) first, then on the real arm at low speed.
- **Stop.** Know how to stop your program (<kbd>Ctrl</kbd>+<kbd>C</kbd> in the launch terminal) and where the power switch is. Neither is a certified emergency stop.

> [!CAUTION]
> **Torque off before you touch it.** Move joints by hand only with torque disabled (driver stopped, or torque switched off in the GUI or DYNAMIXEL Wizard). When torque goes off, the arm drops under its own weight, so support it first.

## Troubleshooting

| Problem | What to try | Source |
| --- | --- | --- |
| Permission denied on `/dev/ttyUSB0` | Add yourself to the `dialout` group (`sudo usermod -aG dialout $USER`), then log out and back in | [Quick start](https://docs.robotis.com/docs/systems/openmanipulator_x/quick_start_guide/) |
| Jerky or slow communication | The USB latency timer is still 16 ms. Run `om_create_udev_rules`, reconnect the U2D2 and check `latency_timer` reads 1 | [Quick start](https://docs.robotis.com/docs/systems/openmanipulator_x/quick_start_guide/) |
| LEDs don't blink at power-on | Check the power supply, switch and cable seating | [Quick start](https://docs.robotis.com/docs/systems/openmanipulator_x/quick_start_guide/) |
| ROS 2 can't find the servos | Check the port (`/dev/ttyUSB0` for the U2D2, `/dev/ttyACM0` for OpenCR). Scan in DYNAMIXEL Wizard for IDs 11-15 at 1 Mbps; make sure each ID is unique; try other baud rates; try Firmware Recovery | [DYNAMIXEL FAQ](https://docs.robotis.com/docs/faq/faq_dynamixel), [basic operation](https://docs.robotis.com/docs/systems/openmanipulator_x/quick_start_guide/basic_operation) |
| The arm won't move after launch | A joint started outside its range. Stop, move it to the start pose with torque off, relaunch | [Basic operation](https://docs.robotis.com/docs/systems/openmanipulator_x/quick_start_guide/basic_operation) |
| DYNAMIXEL Wizard can't change an ID | Turn torque off first (EEPROM is locked while torque is on) | [XM430-W350 reference](https://docs.robotis.com/docs/dxl/model_reference/x_series/xm_series/xm430-w350) |
| OpenCR upload fails | Recovery mode: hold PUSH SW2, press and release Reset, release SW2; the status LED blinks every 100 ms | [Quick start](https://docs.robotis.com/docs/systems/openmanipulator_x/quick_start_guide/) |

## Resources

- Official: [OpenManipulator-X on ROBOTIS Docs](https://docs.robotis.com/docs/systems/openmanipulator_x/overview/) · [specification](https://docs.robotis.com/docs/systems/openmanipulator_x/specification/) · [quick start](https://docs.robotis.com/docs/systems/openmanipulator_x/quick_start_guide/) · [DYNAMIXEL Wizard 2.0](https://docs.robotis.com/docs/software/dynamixel_wizard_2_0/introduction) · [U2D2](https://docs.robotis.com/docs/parts/interface/u2d2) · [U2D2 Power Hub Board](https://docs.robotis.com/docs/parts/interface/u2d2_power_hub) · [DYNAMIXEL FAQ](https://docs.robotis.com/docs/faq/faq_dynamixel)
- Code: [ROBOTIS-GIT/open_manipulator](https://github.com/ROBOTIS-GIT/open_manipulator) · [DynamixelSDK](https://github.com/ROBOTIS-GIT/DynamixelSDK) · [robotis_mujoco_menagerie](https://github.com/ROBOTIS-GIT/robotis_mujoco_menagerie)
- Legacy: the [old e-Manual page](https://emanual.robotis.com/docs/en/platform/openmanipulator_x/overview/), while it lasts
- Lab: [ATR-Lab/multi-servo-dynamixel-library](https://github.com/ATR-Lab/multi-servo-dynamixel-library) · [lab robots and ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md)

## Related

- [Lab hardware index](README.md) and the [checklist before you use any hardware](README.md#before-you-use-any-hardware)
- [SO-101 arms](lerobot-so-101.md), the lab's other arm
- [Lab safety rules](../lab-rules/safety.md)
- Tech stack: [ROS 2](../tech-stack/ros2.md) · [Gazebo](../tech-stack/gazebo.md) · [MuJoCo](../tech-stack/mujoco.md) · [Docker](../tech-stack/docker.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/hardware/openmanipulator-x.md)</sub>
