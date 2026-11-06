# MuJoCo

> **Read this when** you need a fast, accurate physics simulator for control or learning, want a ready-made model of a lab robot, or want to train on a GPU with MJX or MuJoCo Warp.

[MuJoCo](https://mujoco.org/) (Multi-Joint dynamics with Contact) is an open-source physics engine maintained by Google DeepMind, widely used in robotics research for control and reinforcement learning. It installs with one `pip` command, runs on a laptop (macOS, Linux or Windows) and comes with [MuJoCo Menagerie](https://github.com/google-deepmind/mujoco_menagerie), a collection of checked robot models. The one thing to remember: MuJoCo is the quickest way to try a controller on a lab robot's model before you go near the hardware.

## Contents

- [Versions and packages](#versions-and-packages)
- [Install and first run](#install-and-first-run)
- [Models of lab robots in Menagerie](#models-of-lab-robots-in-menagerie)
- [GPU simulation: MJX and MuJoCo Warp](#gpu-simulation-mjx-and-mujoco-warp)
- [Lab notes](#lab-notes)
- [Related](#related)

## Versions and packages

Checked on Sept. 30, 2026:

| Package | Version | What it is | Install |
| --- | --- | --- | --- |
| `mujoco` | **3.14.0** (Sept. 22, 2026) | The engine and its Python bindings; Python 3.10 or later | `pip install mujoco` |
| `mujoco-mjx` | 3.14.0 | MJX: MuJoCo rewritten in JAX, for many simulations in parallel on a GPU or TPU | `pip install mujoco-mjx` |
| `mujoco-warp` | 3.14.0 | MuJoCo Warp (MJWarp): a GPU version for NVIDIA hardware, maintained by Google DeepMind and NVIDIA | `pip install mujoco-warp` |
| `playground` | 0.2.0 | [MuJoCo Playground](https://github.com/google-deepmind/mujoco_playground): ready-made learning environments on MJX; Python 3.11 or later | `pip install playground` |
| `mujoco-menagerie` | 2026.9.0 | Downloads and loads Menagerie models by name | `pip install mujoco-menagerie` |

Sources: [MuJoCo releases](https://github.com/google-deepmind/mujoco/releases), [Python docs](https://mujoco.readthedocs.io/en/latest/python.html), [MJX docs](https://mujoco.readthedocs.io/en/latest/mjx.html), [MuJoCo Warp](https://github.com/google-deepmind/mujoco_warp) and the [Menagerie README](https://github.com/google-deepmind/mujoco_menagerie#readme). MuJoCo is Apache 2.0; each Menagerie model carries its own license file.

## Install and first run

For Ubuntu, macOS or Windows, in a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install mujoco
# Open the interactive viewer with an empty scene
python -m mujoco.viewer
```

To look at a lab robot's model, clone Menagerie and open its scene file (the command the Menagerie README gives):

```bash
git clone https://github.com/google-deepmind/mujoco_menagerie.git
python -m mujoco.viewer --mjcf mujoco_menagerie/unitree_go2/scene.xml
```

On macOS, use `mjpython` instead of `python` for the passive viewer when you launch it from your own script; the [Python docs](https://mujoco.readthedocs.io/en/latest/python.html) explain why.

A minimal simulation loop in Python:

```python
import mujoco

model = mujoco.MjModel.from_xml_path("mujoco_menagerie/unitree_go2/scene.xml")
data = mujoco.MjData(model)

for _ in range(1000):
    mujoco.mj_step(model, data)  # advance the simulation by one time step

print(data.qpos)  # joint positions after 1,000 steps
```

## Models of lab robots in Menagerie

Checked against the [Menagerie repository](https://github.com/google-deepmind/mujoco_menagerie) on Sept. 30, 2026:

| Lab robot | Menagerie folder | License | Notes |
| --- | --- | --- | --- |
| Unitree Go2 | `unitree_go2` | BSD-3-Clause | Also an MJX-ready version (`go2_mjx.xml`, `scene_mjx.xml`) |
| Booster K1 | None | | Menagerie has the larger Booster T1 (`booster_t1`); a K1 model has to come from Booster's own files |
| LeRobot SO-101 | `robotstudio_so101` | Apache 2.0 | The earlier SO-100 is `trs_so_arm100` |
| ROBOTIS OpenManipulator-X | None | | Menagerie has other ROBOTIS models (`robotis_op3` humanoid, `robotis_omy_3m` arm) but not the OpenManipulator-X |

Menagerie also has the Unitree G1 and H1 humanoids, Franka arms and Hello Robot Stretch. Menagerie models are simplified for simulation; check masses, joint limits and actuator gains against the real robot before you trust a result.

## GPU simulation: MJX and MuJoCo Warp

For reinforcement learning you usually need thousands of simulations at once. Two options run MuJoCo on the GPU:

- **MJX** is written in JAX and runs on "Nvidia and AMD GPUs, Apple Silicon, and Google Cloud TPUs" ([MJX docs](https://mujoco.readthedocs.io/en/latest/mjx.html)). MuJoCo Playground's environments use it. Models often need simplifying (fewer contacts, simpler collision shapes) to run fast; the Go2 has a ready `scene_mjx.xml`.
- **MuJoCo Warp** is written in NVIDIA Warp for NVIDIA GPUs and handles contacts faster; MJX can use it as a backend (`pip install mujoco-mjx[warp]`). Unlike MJX on JAX, it does not support automatic differentiation.

Book GPU time on the lab machines before long runs ([shared machines and GPUs](../lab-rules/best-practices.md#shared-machines-and-gpus)).

## Lab notes

- Lab robot models the lab has tuned or built: [location of lab MuJoCo models].
- When you report results, say which model you used (Menagerie folder and commit, or the lab's own model) and that the results are from simulation.

## Related

- [Tech stack](README.md)
- [Isaac Sim and Isaac Lab](isaac-sim.md) and [Gazebo](gazebo.md): other simulators the lab uses
- [LeRobot](lerobot.md): learning on the real SO-101 arms
- [Research standards: reproducibility](../research/standards.md#reproducibility-and-artifacts)
- [MuJoCo documentation](https://mujoco.readthedocs.io/)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/tech-stack/mujoco.md)</sub>
