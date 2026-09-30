# Unity

> **Read this when** you are building an XR (virtual or mixed reality) teleoperation interface, a Meta Quest app or a Unity scene that has to talk to a ROS 2 robot.

[Unity](https://unity.com/) is a game engine that the lab uses for XR interfaces, such as the Meta Quest interface of TeleBot-4R ([TeleBot-4R-XR](https://github.com/ATR-Lab/TeleBot-4R-XR)), where an operator sees through the robot and controls it with a headset and hand controllers. The hard part is rarely Unity itself; it is the link to ROS 2, where the older Unity packages are no longer maintained. The one thing to remember: pick the ROS connection first, with your mentor, before you pick a Unity version.

## Contents

- [Versions and licenses](#versions-and-licenses)
- [Set up Unity for Meta Quest](#set-up-unity-for-meta-quest)
- [Connecting Unity to ROS 2](#connecting-unity-to-ros-2)
- [Lab notes](#lab-notes)
- [Related](#related)

## Versions and licenses

Checked on Sept. 30, 2026, on [Unity 6 releases](https://unity.com/releases/unity-6):

| Version | Support | Use it for |
| --- | --- | --- |
| **Unity 6.3 LTS** (6000.3) | Long-term support until December 2027 | New lab projects: the current long-term-support release |
| Unity 6.0 LTS (6000.0) | Supported through October 2026 | Existing projects only; plan to move them to 6.3 |
| Newer 6.x update releases | Shorter support | Only if a package you need requires one |

Install Unity through Unity Hub and pin the exact editor version (for example `6000.3.x`) in the project's README, so everyone opens the project with the same one.

**Licenses.** Students can get the free [Unity Student plan](https://unity.com/products/unity-student): one year, renewable, verified through SheerID, for students 16 and older enrolled at an accredited institution. Faculty and staff have the [Unity Educator plan](https://unity.com/products/unity-educator), and institutions can apply for the [Education Grant License](https://unity.com/products/unity-education-grant-license) (multi-seat, non-commercial only). The lab's arrangement: [which Unity license lab machines use].

## Set up Unity for Meta Quest

From Meta's [Unity project setup guide](https://developers.meta.com/horizon/documentation/unity/unity-project-setup/):

1. Use Unity Editor 6000.0.66f2 or later; Meta recommends 6.1 or later, so Unity 6.3 LTS fits.
2. Install the **Meta XR Core SDK** and the **Meta XR Platform SDK**, and use the **Unity OpenXR Plugin** as the XR provider. The older Oculus XR Plugin is deprecated and scheduled for removal.
3. Set the build target to **Meta Quest** (or Android on older editors).
4. Install [Meta Quest Developer Hub](https://developers.meta.com/horizon/documentation/unity/ts-mqdh-getting-started/), a companion app for Windows and macOS, to manage headsets, install builds and read logs.

Headsets need developer mode turned on through a Meta developer account; ask [lab manager name] which lab headsets are already set up.

## Connecting Unity to ROS 2

Status of the common options, checked on GitHub on Sept. 30, 2026:

| Option | How it connects | Status |
| --- | --- | --- |
| [ROS-TCP-Connector](https://github.com/Unity-Technologies/ROS-TCP-Connector) and ROS-TCP-Endpoint (Unity Robotics Hub) | TCP to a ROS-side endpoint node | Last release v0.7.0, February 2022; the README still lists ROS 2 Foxy and Galactic. Unity has moved this workflow to the hub's [archive page](https://github.com/Unity-Technologies/Unity-Robotics-Hub/blob/main/ARCHIVE.md). Treat it as unmaintained |
| [Unity Robotics Hub](https://github.com/Unity-Technologies/Unity-Robotics-Hub): Simulation Pro | Unity's new robotics package with URDF import, sensors and ROS 2 support | Early access for Unity Industry developers; "supported for production on Unity 6.3 and newer" |
| [ROS#](https://github.com/siemens/ros-sharp) with [rosbridge_suite](https://github.com/RobotWebTools/rosbridge_suite) | WebSocket to a rosbridge server on the robot's ROS 2 side | Maintained: ROS# 2.3.0 (Sept. 9, 2026) and rosbridge_suite 4.2.1, with Humble, Jazzy and Kilted branches. ROS# is built with Unity 2022.3 LTS; its README says Unity 6 "has not yet been thoroughly tested" |
| [ros2-for-unity](https://github.com/RobotecAI/ros2-for-unity) | Native ROS 2 (DDS) inside Unity | Its README says the team is "unable to provide support and maintain the project for the general community" |

For a new project, the rosbridge route is the most actively maintained today, at the cost of WebSocket latency (the delay between an action and the robot's response). Measure latency for your task before you build a teleoperation study on it. Whichever option you choose, write it and its version in the project README.

## Lab notes

- Lab headsets and where they are kept: [Meta Quest headsets and location].
- Project code style for C# and Unity: see the [dev guidelines](https://github.com/ATR-Lab/dev-guidelines).
- When you show an XR teleoperation demo, label it as teleoperated, and say whether the video is live or recorded.

## Related

- [Tech stack](README.md)
- [ROS 2](ros2.md)
- [TeleBot-4R-XR](https://github.com/ATR-Lab/TeleBot-4R-XR), the lab's Meta Quest interface for TeleBot-4R
- [Autodesk Fusion and Inventor](autodesk.md): models and meshes for Unity scenes

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/tech-stack/unity.md)</sub>
