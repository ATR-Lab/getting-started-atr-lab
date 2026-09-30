# Gazebo

> **Read this when** you want to simulate a robot with ROS 2, need to know which Gazebo release goes with your ROS 2 distribution, or are moving an old Gazebo Classic project.

[Gazebo](https://gazebosim.org/) is the open-source robot simulator from Open Robotics that ROS 2 is designed around: it simulates robots, sensors and worlds, and `ros_gz` connects its topics to ROS 2. It runs on an ordinary Linux laptop, which makes it the usual first simulator for ROS 2 work. The one thing to remember: each ROS 2 distribution has one recommended Gazebo release, and mixing others causes most "it won't build" problems.

## Contents

- [Releases](#releases)
- [Which Gazebo goes with which ROS 2](#which-gazebo-goes-with-which-ros-2)
- [Install and first run](#install-and-first-run)
- [Bridge Gazebo and ROS 2 topics](#bridge-gazebo-and-ros-2-topics)
- [Gazebo Classic is retired](#gazebo-classic-is-retired)
- [Related](#related)

## Releases

From Gazebo's [releases page](https://gazebosim.org/docs/latest/releases/), checked Sept. 30, 2026:

| Release | Released | End of life | Support |
| --- | --- | --- | --- |
| Jetty | Sept. 2025 | May 2031 | Long-term support (LTS) |
| Ionic | Sept. 2024 | Dec. 2026 | Standard |
| Harmonic | Sept. 2023 | May 2029 | LTS |
| Fortress | Sept. 2021 | May 2027 | LTS |
| "M" (name not yet announced) | Planned March 2027 | Planned Dec. 2028 | |

## Which Gazebo goes with which ROS 2

From Gazebo's [ROS installation page](https://gazebosim.org/docs/latest/ros_installation/). Use the recommended pairing; the others are possible but need care, and many combinations don't work at all.

| ROS 2 distribution | Recommended Gazebo | Also possible, with caution |
| --- | --- | --- |
| Humble (LTS) | Fortress | Harmonic |
| Jazzy (LTS) | Harmonic | |
| Kilted | Ionic | Harmonic |
| Lyrical (LTS) | Jetty | Harmonic, Ionic |
| Rolling | Jetty | Harmonic, Ionic |

Which ROS 2 distribution the lab uses for each robot is in [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2).

## Install and first run

With ROS 2 already installed on Ubuntu, install `ros_gz` for your distribution. Since ROS 2 Jazzy, this also installs the matching Gazebo release from the ROS package repository:

```bash
# Ubuntu 24.04 with ROS 2 Jazzy: installs ros_gz and Gazebo Harmonic
sudo apt-get install ros-jazzy-ros-gz
```

Start Gazebo from ROS 2 with a sample world (from the [`ros_gz_sim` README](https://github.com/gazebosim/ros_gz/tree/jazzy/ros_gz_sim)):

```bash
source /opt/ros/jazzy/setup.bash
ros2 launch ros_gz_sim gz_sim.launch.py gz_args:="shapes.sdf"
```

To run Gazebo in a container instead, see [GUI apps from a container](docker.md#run-gui-apps-from-a-container).

## Bridge Gazebo and ROS 2 topics

Gazebo has its own message system; `ros_gz_bridge` copies messages between it and ROS 2. For example, to share the simulation clock with ROS 2 nodes (from the [`ros_gz_bridge` README](https://github.com/gazebosim/ros_gz/tree/jazzy/ros_gz_bridge)):

```bash
ros2 run ros_gz_bridge parameter_bridge /clock@rosgraph_msgs/msg/Clock[gz.msgs.Clock
```

The part after the topic name gives the ROS 2 type, a direction symbol (`[` means Gazebo to ROS 2, `]` means ROS 2 to Gazebo, `@` means both ways) and the Gazebo type. For more than a few topics, list them in a YAML file; the README shows how. Remember to set `use_sim_time:=true` on nodes that should follow the simulation clock.

## Gazebo Classic is retired

Gazebo Classic (the old `gazebo` 11 with `gazebo_ros_pkgs`) reached end of life in January 2025 ([classic.gazebosim.org](https://classic.gazebosim.org/)). It gets no fixes and does not support current ROS 2 distributions. If you inherit a project built on it, plan a migration to the new Gazebo; Gazebo's documentation has migration guides for worlds, models and plugins.

## Related

- [Tech stack](README.md)
- [ROS 2](ros2.md) and [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2)
- [Isaac Sim](isaac-sim.md) and [MuJoCo](mujoco.md): the lab's other simulators
- [Gazebo documentation](https://gazebosim.org/docs/latest/getstarted/)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/tech-stack/gazebo.md)</sub>
