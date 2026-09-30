# SO-101 arms (LeRobot)

> **Read this when** you are about to set up, calibrate, teleoperate or collect data with the lab's SO-101 leader and follower arms, or train a policy for them.

This page covers the SO-101, a low-cost open-source robot arm designed by TheRobotStudio and programmed with Hugging Face's LeRobot library: its parts, motor setup, calibration, leader-follower teleoperation, recording datasets, training a policy and running it on the arm. The one thing to remember: **each arm's calibration is saved under the `id` you give it**, so always use the same ID for the same physical arm in every command.

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

The SO-101 is the "next-generation version of the SO-100 robot arm" from [TheRobotStudio's SO-ARM100 repository](https://github.com/TheRobotStudio/SO-ARM100), with 3D-printed parts and six Feetech STS3215 serial bus servos per arm. It comes as a pair:

- The **leader** arm is the one you move by hand. Its motors use lighter gearing so it is easy to move and can hold its own weight.
- The **follower** arm copies the leader's joint positions. It is the robot that does the task.

This pairing is **leader-follower teleoperation**: you control the follower from a distance by moving the leader. Record those demonstrations as a dataset, train a policy (a neural network that maps camera images and joint positions to motor commands) and the follower then runs the task on its own. Label every demo and video as teleoperated (leader driving follower) or autonomous (a trained policy driving it).

The software is [LeRobot](https://huggingface.co/docs/lerobot/so101), Hugging Face's open-source library for real-world robot learning. Lab guide: [LeRobot](../tech-stack/lerobot.md).

What the lab uses it for: `[current SO-101 projects and who leads them]`.

## Key specs

TheRobotStudio and LeRobot publish parts and motors, not performance figures: reach, payload, weight and repeatability are not published. Checked Sept. 30, 2026 against the [SO-ARM100 README](https://github.com/TheRobotStudio/SO-ARM100) and the [LeRobot SO-101 guide](https://huggingface.co/docs/lerobot/so101).

| Spec | Leader arm | Follower arm |
| --- | --- | --- |
| Motors | Six Feetech STS3215 | Six Feetech STS3215 |
| Gear ratios | Shoulder pan 1/191, shoulder lift 1/345, elbow flex 1/191, wrist flex 1/147, wrist roll 1/147, gripper 1/147 | All six 1/345 |
| Motor voltage | Always the 7.4 V version | 7.4 V version, or the higher-torque 12 V version |
| Stall torque (README) | Not listed per joint | 16.5 kg·cm at 6 V (7.4 V version); 30 kg·cm (12 V version) |
| Power supply | 5 V supply | 5 V supply for 7.4 V motors; "12V 5A+" supply for 12 V motors |
| Controller | One motor control board (serial bus servo driver, for example Waveshare) with USB-C | Same |
| Motor IDs | 1 (shoulder pan) to 6 (gripper), set by LeRobot | Same |
| Bus speed | 1,000,000 baud (LeRobot's Feetech default) | Same |
| Printed parts | PLA+; 0.4 mm nozzle at 0.2 mm layers, or 0.6 mm at 0.4 mm; 15% infill; supports | Same |
| License | Apache-2.0 (hardware repo) | Same |

The README's reference prices were $121.94 for one follower arm and $229.88 for a leader and follower pair (US parts, checked Sept. 30, 2026).

## In our lab

| Item | Details |
| --- | --- |
| Quantity | `[N leader arms, N follower arms]` |
| Follower motor version | `[7.4 V or 12 V follower motors]` (this sets which power supply to use) |
| Location | `[Room ###, bench or shelf]` |
| Owner or contact | `[SO-101 owner or contact name]` |
| Checkout | `[checkout procedure]` |
| Arm IDs | `[the calibration ID written on each arm's label]` |
| Cameras | `[which cameras go with the arms]` |
| Accounts and credentials | Hugging Face datasets and models go to `[lab Hugging Face organization]`. Ask `[lab manager name]` for access; never commit Hugging Face or Weights & Biases tokens to any repo |
| Lab repos | `[lab SO-101 repo, if any]` |

## First steps

These steps follow the [LeRobot SO-101 guide](https://huggingface.co/docs/lerobot/so101) (LeRobot v0.6.1, the latest release on PyPI on Sept. 30, 2026). If the arms are already assembled, set up and calibrated, skip to step 5 and ask `[SO-101 owner or contact name]` for the IDs.

1. **Finish the [hardware checklist](README.md#before-you-use-any-hardware)** and read [Safety](#safety) below.
2. **Install LeRobot.** It needs Python 3.12 or later ([installation guide](https://huggingface.co/docs/lerobot/installation)):

   ```bash
   # Ubuntu 24.04 or macOS, in a conda (Miniforge) environment
   conda create -y -n lerobot python=3.12
   conda activate lerobot
   conda install ffmpeg -c conda-forge
   git clone https://github.com/huggingface/lerobot.git
   cd lerobot
   pip install -e ".[core_scripts]"
   # Feetech motor support for the SO-101
   pip install -e ".[feetech]"
   ```

3. **Find each arm's USB port.** Connect one controller board by USB and power, run the command below and unplug the board when it asks:

   ```bash
   # In the lerobot environment (Linux or macOS)
   lerobot-find-port
   ```

   On Linux, the ports look like `/dev/ttyACM0`; give your user access to them:

   ```bash
   sudo chmod 666 /dev/ttyACM0
   sudo chmod 666 /dev/ttyACM1
   ```

4. **Set motor IDs (new motors only).** New motors all start with ID 1. The setup script asks you to connect **one motor at a time** (starting with the gripper) and writes its ID and baud rate. Replace the ports with yours:

   ```bash
   # Follower arm
   lerobot-setup-motors --robot.type=so101_follower --robot.port=/dev/ttyACM0

   # Leader arm
   lerobot-setup-motors --teleop.type=so101_leader --teleop.port=/dev/ttyACM1
   ```

5. **Calibrate each arm.** Move the arm so every joint is in the middle of its range, press Enter, then move each joint through its full range. The `id` names the calibration file; the IDs below are examples:

   ```bash
   lerobot-calibrate --robot.type=so101_follower --robot.port=/dev/ttyACM0 --robot.id=my_follower_arm

   lerobot-calibrate --teleop.type=so101_leader --teleop.port=/dev/ttyACM1 --teleop.id=my_leader_arm
   ```

6. **Teleoperate.** Moving the leader now moves the follower ([real-world robots guide](https://huggingface.co/docs/lerobot/il_robots)):

   ```bash
   lerobot-teleoperate \
       --robot.type=so101_follower \
       --robot.port=/dev/ttyACM0 \
       --robot.id=my_follower_arm \
       --teleop.type=so101_leader \
       --teleop.port=/dev/ttyACM1 \
       --teleop.id=my_leader_arm
   ```

> [!NOTE]
> Two command examples in the LeRobot docs (checked Sept. 30, 2026) break if you paste them into bash: the `lerobot-calibrate` examples put a `# comment` after a line-continuation backslash, and the `lerobot-record` example has a commented-out line inside the command. The commands on this page have those comments removed.

## Software

### Cameras, datasets, training and running a policy

All commands below come from LeRobot's [real-world robots guide](https://huggingface.co/docs/lerobot/il_robots) and [cameras guide](https://huggingface.co/docs/lerobot/cameras); ports, IDs and names are examples.

**Find cameras**, then add them to teleoperation or recording with `--robot.cameras`:

```bash
lerobot-find-cameras opencv
```

**Log in to Hugging Face.** Keep the token in an environment variable, never in a file you commit:

```bash
hf auth login --token ${HUGGINGFACE_TOKEN} --add-to-git-credential
HF_USER=$(NO_COLOR=1 hf auth whoami | awk -F': *' 'NR==1 {print $2}')
echo $HF_USER
```

**Record a dataset** of teleoperated demonstrations. LeRobot suggests "at least 50 episodes" for a task. During recording, the right arrow key (or <kbd>n</kbd>) moves to the next episode, the left arrow (or <kbd>r</kbd>) re-records and <kbd>Esc</kbd> (or <kbd>q</kbd>) stops:

```bash
lerobot-record \
    --robot.type=so101_follower \
    --robot.port=/dev/ttyACM0 \
    --robot.id=my_follower_arm \
    --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 1920, height: 1080, fps: 30}}" \
    --teleop.type=so101_leader \
    --teleop.port=/dev/ttyACM1 \
    --teleop.id=my_leader_arm \
    --display_data=true \
    --dataset.repo_id=${HF_USER}/record-test \
    --dataset.num_episodes=5 \
    --dataset.single_task="Grab the black cube" \
    --dataset.streaming_encoding=true \
    --dataset.encoder_threads=2
```

> [!IMPORTANT]
> Recording **uploads the dataset to the Hugging Face Hub by default**. If a camera can see people, or the data belongs to a study, add `--dataset.push_to_hub=False` and ask `[lab manager name]` before you share it. Human-subjects data follows the lab's research standards and IRB approval.

**Replay** an episode on the follower:

```bash
lerobot-replay \
    --robot.type=so101_follower \
    --robot.port=/dev/ttyACM0 \
    --robot.id=my_follower_arm \
    --dataset.repo_id=${HF_USER}/record-test \
    --dataset.episode=0
```

**Train a policy** (ACT shown here) on a machine with an NVIDIA GPU (`--policy.device=cuda`; use `mps` on Apple silicon). Use the same dataset name you recorded. The trained model is pushed to the Hub unless you add `--policy.push_to_hub=false`:

```bash
lerobot-train \
  --dataset.repo_id=${HF_USER}/record-test \
  --policy.type=act \
  --output_dir=outputs/train/act_so101_test \
  --job_name=act_so101_test \
  --policy.device=cuda \
  --wandb.enable=true \
  --policy.repo_id=${HF_USER}/my_policy
```

**Run the trained policy** on the follower with `lerobot-rollout`. The docs' example uses `so100_follower`; for our arms pass `so101_follower`, which LeRobot v0.6.1 registers as a robot type. With a policy in control, the arm moves **autonomously**:

```bash
lerobot-rollout \
  --strategy.type=base \
  --policy.path=${HF_USER}/my_policy \
  --robot.type=so101_follower \
  --robot.port=/dev/ttyACM0 \
  --robot.cameras="{ front: {type: opencv, index_or_path: 0, width: 640, height: 480, fps: 30}}" \
  --task="Grab the black cube" \
  --duration=60
```

The `sentry` strategy (with `--dataset.repo_id=${HF_USER}/eval_...`) records evaluation episodes while the policy runs.

### Simulation models

| Model | What it gives you | Link |
| --- | --- | --- |
| MuJoCo Menagerie `robotstudio_so101` | MJCF follower model (Apache-2.0), MuJoCo 3.1.3 or later | [robotstudio_so101](https://github.com/google-deepmind/mujoco_menagerie/tree/main/robotstudio_so101) |
| SO-ARM100 `Simulation/SO101` | URDF and MJCF files from TheRobotStudio, plus a leader-arm URDF | [Simulation/SO101](https://github.com/TheRobotStudio/SO-ARM100/tree/main/Simulation/SO101) |
| LeIsaac on LeRobot EnvHub | SO-101 tasks in Isaac Lab, such as `LeIsaac-SO101-PickOrange-v0` | [LeIsaac guide](https://huggingface.co/docs/lerobot/envhub_leisaac) |

Lab guides: [MuJoCo](../tech-stack/mujoco.md), [Isaac Sim](../tech-stack/isaac-sim.md).

### Printing and building parts

The [SO-ARM100 README](https://github.com/TheRobotStudio/SO-ARM100) gives print settings for FDM printers with PLA+ and links the step-by-step [assembly guide](https://huggingface.co/docs/lerobot/so101). The lab's [Formlabs Form 3](formlabs-form-3.md) is a resin printer, and the repo gives no resin settings.

## Safety

Read the lab's safety rules first, especially [robots in motion](../lab-rules/safety.md#robots-in-motion). Neither TheRobotStudio nor LeRobot publishes pinch-point or emergency-stop guidance for the SO-101, so most rules below are lab practice.

> [!WARNING]
> **The follower moves whenever the leader moves, and whenever a policy runs.** Keep hands, hair and cables out of the follower's reach while a teleoperation, recording or rollout command is running. Joints and the gripper are pinch points. To stop, press <kbd>Ctrl</kbd>+<kbd>C</kbd> in the terminal or switch off the follower's power supply.

- **Torque off before you touch the follower.** LeRobot turns motor torque off when the program disconnects (`disable_torque_on_disconnect` is on by default in the follower config), so the arm can drop when a command ends. Support it.
- **One motor at a time during setup.** "Make sure it's the only motor connected to the board", and check the cabling at each step.
- **Motor firmware.** LeRobot's [Feetech guide](https://huggingface.co/docs/lerobot/feetech): "Do not disconnect power or USB during firmware updates."
- **First policy runs.** Clear the table of anything fragile, stand where you can reach the power switch and start with short runs (`--duration`). The follower config also has a `max_relative_target` option that caps how far each command can move a joint.

> [!CAUTION]
> **Match the power supply to the motors.** The README says to use a "12V 5A+ power supply instead of a 5V one" for 12 V follower motors, and "The leader arm is always 7.4V". A supply of the wrong voltage can damage the motors. Check the label before you plug in.

## Troubleshooting

| Problem | What to try | Source |
| --- | --- | --- |
| Permission denied on `/dev/ttyACM0` (Linux) | `sudo chmod 666 /dev/ttyACM0` (and the second port) | [SO-101 guide](https://huggingface.co/docs/lerobot/so101) |
| `lerobot-setup-motors` errors | Check the power supply, the USB cable and the 3-pin motor cable. On a Waveshare board, set both jumpers to the `B` channel (USB) | [SO-101 guide](https://huggingface.co/docs/lerobot/so101) |
| Reused motors don't respond | Their IDs and baud rate likely don't match: run the motor setup again | [SO-101 guide](https://huggingface.co/docs/lerobot/so101) |
| Teleoperation asks you to calibrate again | You used a different `id` from the one you calibrated with. Use the same IDs in every command | [LeRobot cheat sheet](https://huggingface.co/docs/lerobot/cheat-sheet) |
| Recording keys (arrows, Esc) do nothing | Run `lerobot-record` in an interactive terminal and keep it focused; the letter keys also work | [Real-world robots guide](https://huggingface.co/docs/lerobot/il_robots) |
| Keyboard teleoperation doesn't work on Linux | It needs an X11 session; it is unavailable on Wayland or headless machines | [Real-world robots guide](https://huggingface.co/docs/lerobot/il_robots) |
| `pip install` fails building video libraries (Linux) | Install the build dependencies listed in the installation guide's troubleshooting section | [Installation](https://huggingface.co/docs/lerobot/installation) |

## Resources

- Hardware: [TheRobotStudio/SO-ARM100](https://github.com/TheRobotStudio/SO-ARM100) (bill of materials, print files, simulation)
- Software: [LeRobot SO-101 guide](https://huggingface.co/docs/lerobot/so101) · [real-world robots guide](https://huggingface.co/docs/lerobot/il_robots) · [installation](https://huggingface.co/docs/lerobot/installation) · [cameras](https://huggingface.co/docs/lerobot/cameras) · [Feetech motors](https://huggingface.co/docs/lerobot/feetech) · [huggingface/lerobot](https://github.com/huggingface/lerobot) · [lerobot on PyPI](https://pypi.org/project/lerobot/)
- Community: the [LeRobot Discord](https://discord.com/invite/s3KuuzsPFb), linked from the SO-101 guide
- Lab: [lab robots and ROS 2](https://github.com/ATR-Lab/all-things-ros2/blob/main/docs/08-lab-robots.md)

## Related

- [Lab hardware index](README.md) and the [checklist before you use any hardware](README.md#before-you-use-any-hardware)
- [OpenManipulator-X](openmanipulator-x.md), the lab's other arm
- [Jetson AGX Thor](jetson-agx-thor.md), for training and running policies on the robot side
- [Lab safety rules](../lab-rules/safety.md)
- Tech stack: [LeRobot](../tech-stack/lerobot.md) · [MuJoCo](../tech-stack/mujoco.md) · [Isaac Sim](../tech-stack/isaac-sim.md)

<sub>Last reviewed: Sept. 30, 2026 · Sources checked on that date · [Suggest a change](https://github.com/ATR-Lab/getting-started-atr-lab/edit/master/hardware/lerobot-so-101.md)</sub>
