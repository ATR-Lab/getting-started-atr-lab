# LeRobot

> **Read this when** you want to record demonstrations on a robot arm, train a policy that imitates them, or use the lab's SO-101 arms.

[LeRobot](https://github.com/huggingface/lerobot) is Hugging Face's open-source library (Apache 2.0) of "models, datasets, and tools for real-world robotics in PyTorch". In the lab it is the software for the SO-101 arms and a common starting point for imitation learning: you drive a leader arm by hand, the follower arm copies it, LeRobot records what the cameras and motors saw, and a policy (a neural network that maps observations to motor commands) learns to do the task alone. The one thing to remember: `lerobot-record` uploads datasets to the Hugging Face Hub by default, so turn that off for anything that shows people.

## Contents

- [What LeRobot gives you](#what-lerobot-gives-you)
- [Install](#install)
- [The workflow](#the-workflow)
- [Datasets and privacy](#datasets-and-privacy)
- [Policies](#policies)
- [Lab notes](#lab-notes)
- [Related](#related)

## What LeRobot gives you

| Part | What it is |
| --- | --- |
| Hardware drivers | Leader and follower arms and mobile bases, including SO-100, SO-101, Koch, LeKiwi, Reachy 2 and Unitree G1, plus keyboards, gamepads and phones as teleoperators |
| Command-line tools | `lerobot-find-port`, `lerobot-calibrate`, `lerobot-teleoperate`, `lerobot-record`, `lerobot-replay`, `lerobot-train`, `lerobot-eval` and more |
| Dataset format | LeRobotDataset v3.0: Parquet tables for states and actions plus MP4 video, shareable on the [Hugging Face Hub](https://huggingface.co/datasets?other=LeRobot) ([format docs](https://huggingface.co/docs/lerobot/lerobot-dataset-v3)) |
| Policies | Imitation learning, reinforcement learning and vision-language-action models ([below](#policies)) |
| Simulation environments | Optional extras such as `aloha` and `pusht` for testing policies without hardware |

Versions checked on Sept. 30, 2026: the latest release is **0.6.1** (Aug. 3, 2026) on [GitHub](https://github.com/huggingface/lerobot/releases) and [PyPI](https://pypi.org/project/lerobot/), and it needs **Python 3.12 or later**.

## Install

From the [LeRobot installation guide](https://huggingface.co/docs/lerobot/installation), for Ubuntu or macOS with [Miniforge](https://conda-forge.org/download/) (conda):

```bash
conda create -y -n lerobot python=3.12
conda activate lerobot
# ffmpeg decodes the dataset videos; the conda build works with every PyTorch version
conda install ffmpeg -c conda-forge
```

Then install LeRobot with the extras you need:

```bash
# Recording, replaying and calibrating real robots, plus training
pip install 'lerobot[core_scripts,training]'
# Motor support for SO-100 and SO-101 arms (Feetech servos)
pip install 'lerobot[feetech]'
```

To change LeRobot's own code, install from source instead:

```bash
git clone https://github.com/huggingface/lerobot.git
cd lerobot
pip install -e ".[all]"
```

On Linux with an NVIDIA GPU, check that the PyTorch wheel matches the machine's driver; the guide's "PyTorch CUDA variant" section shows how to pick one. Under WSL, also run `conda install evdev -c conda-forge`.

## The workflow

The [imitation learning tutorial](https://huggingface.co/docs/lerobot/il_robots) walks through each step with an SO-101 pair. In short, for Ubuntu (serial ports look like `/dev/ttyACM0`; on macOS they look like `/dev/tty.usbmodem...`):

1. **Find the ports and calibrate** each arm: `lerobot-find-port`, then `lerobot-calibrate`. Use the same `id` for an arm every time, because the calibration file is stored under it. Hardware setup is on the [SO-101 page](../hardware/lerobot-so-101.md) and in the [LeRobot SO-101 guide](https://huggingface.co/docs/lerobot/so101).
2. **Teleoperate** to check that the follower copies the leader:

   ```bash
   lerobot-teleoperate \
     --robot.type=so101_follower \
     --robot.port=[follower port] \
     --robot.id=[follower id] \
     --teleop.type=so101_leader \
     --teleop.port=[leader port] \
     --teleop.id=[leader id]
   ```

3. **Record** episodes of the task with cameras on. Keep it local until you have decided where the data may go:

   ```bash
   lerobot-record \
     --robot.type=so101_follower \
     --robot.port=[follower port] \
     --robot.id=[follower id] \
     --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30}}" \
     --teleop.type=so101_leader \
     --teleop.port=[leader port] \
     --teleop.id=[leader id] \
     --dataset.repo_id=[hf namespace]/[dataset name] \
     --dataset.num_episodes=5 \
     --dataset.single_task="[one-sentence task description]" \
     --dataset.push_to_hub=false
   ```

4. **Train** a policy, for example ACT, on a GPU (see [shared GPUs](../lab-rules/best-practices.md#shared-machines-and-gpus)):

   ```bash
   lerobot-train \
     --dataset.repo_id=[hf namespace]/[dataset name] \
     --policy.type=act \
     --output_dir=outputs/train/[run name] \
     --job_name=[run name] \
     --policy.device=cuda \
     --policy.push_to_hub=false
   ```

5. **Evaluate** the trained policy on the robot with a person at the stop switch, and log every run: which checkpoint, how many trials, how many succeeded.

> [!WARNING]
> A trained policy can move the arm in ways you did not demonstrate. Clear the workspace, keep your hands out of reach while it runs, start at low speed and keep one hand on the power switch. The arm-specific rules are in the [SO-101 safety section](../hardware/lerobot-so-101.md#safety) and the general ones in [robots in motion](../lab-rules/safety.md#robots-in-motion).

## Datasets and privacy

- `lerobot-record` pushes the dataset to the Hugging Face Hub at the end of a session unless you pass `--dataset.push_to_hub=false`. Local copies live in `~/.cache/huggingface/lerobot/`.
- Camera footage that shows people is research data about those people. Do not upload it anywhere public, and if it comes from a study, store it only where the IRB protocol says ([data management](../research/standards.md#data-management)).
- Publish a dataset or model under the lab's Hugging Face namespace, [lab Hugging Face organization], only after your advisor agrees, with a dataset card that says what the task is, how it was collected (teleoperated demonstrations) and its license.
- Hugging Face access tokens are passwords. Log in with `hf auth login` on your own account and never commit a token to a repository.

## Policies

LeRobot's [README](https://github.com/huggingface/lerobot#readme) lists the policies it implements (checked Sept. 30, 2026). A selection:

| Family | Examples | Notes |
| --- | --- | --- |
| Imitation learning | ACT, Diffusion Policy, VQ-BeT | ACT is the usual first choice for a single SO-101 task |
| Reinforcement learning | HIL-SERL, TD-MPC | HIL-SERL learns on the real robot with human interventions |
| Vision-language-action models | Pi0, Pi0.5, SmolVLA, GR00T N1.7 | Large models that take a language instruction; they need more GPU memory. Install extras such as `lerobot[pi]` or `lerobot[smolvla]` |

The [compute hardware guide](https://huggingface.co/docs/lerobot/hardware_guide) lists the GPU memory and training time each policy needs.

## Lab notes

- SO-101 arms, their location and who looks after them: [SO-101 page](../hardware/lerobot-so-101.md).
- Lab Hugging Face organization: [lab Hugging Face organization].
- When you report results, say that the policy runs autonomously after training on teleoperated demonstrations, and give the number of demonstrations and trials.

## Related

- [Tech stack](README.md)
- [LeRobot SO-101 hardware page](../hardware/lerobot-so-101.md)
- [MuJoCo](mujoco.md) and [Isaac Sim and Isaac Lab](isaac-sim.md): simulators for training before the real robot
- [Research standards](../research/standards.md): data management and reproducibility
- [LeRobot documentation](https://huggingface.co/docs/lerobot)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/tech-stack/lerobot.md)</sub>
