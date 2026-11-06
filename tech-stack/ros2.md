# ROS 2

> **Read this when** you need ROS 2 for a robot, a simulator or a class project and want to know where the lab's guide lives and what to read first.

ROS 2 (Robot Operating System 2) is the open-source middleware most lab robots run on: programs called nodes pass messages over topics, services and actions, so a camera driver, a planner and a teleoperation interface can be written separately and still work together. The lab keeps its full ROS 2 guide in a separate repository, [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2), so this page only tells you where to start.

## What to read first

Open [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2) and read, in this order:

1. **The README's quick start**: the lab's default ROS 2 distribution and a five-minute "hello, talker and listener" run.
2. **What ROS 2 is**: nodes, topics, services, actions, parameters, launch files, QoS (quality of service) and tf2 (coordinate frames), with a diagram.
3. **Distributions**: which ROS 2 release runs on which Ubuntu version, when each reaches end of life, and which lab robot needs which.
4. **Install**: natively with apt, or in a container with [ROSEnv](docker.md#rosenv-for-ros-2-projects). Pick one with your mentor.
5. **The cheat sheet and debugging guide**: keep these open while you work.
6. **Lab robots**: each robot's ROS 2 driver and the lab repository that goes with it.

The official documentation is at [docs.ros.org](https://docs.ros.org/en/jazzy/); the lab guide links to the right pages for each topic.

## Where ROS 2 fits in the lab

- **Hardware:** most robots in the [hardware pages](../hardware/README.md) ship a ROS 2 driver or bridge; each page says which distribution it supports.
- **Simulation:** [Gazebo](gazebo.md) pairs with each ROS 2 release through `ros_gz`, and [Isaac Sim](isaac-sim.md) has its own ROS 2 bridge.
- **Tooling:** containers ([Docker](docker.md)) keep one project's ROS 2 distribution from breaking another's. Code style for ROS 2 packages is in the [dev guidelines](https://github.com/ATR-Lab/dev-guidelines).

## Related

- [All things ROS 2](https://github.com/ATR-Lab/all-things-ros2)
- [Tech stack](README.md)
- [Docker and ROSEnv](docker.md)
- [Gazebo](gazebo.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/tech-stack/ros2.md)</sub>
