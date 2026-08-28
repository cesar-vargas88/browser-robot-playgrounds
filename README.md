# browser-robot-playgrounds

> Zero-install browser playgrounds for Physical AI — learn the robot loop in 10 seconds, anywhere.

Real robot learning needs Python + MuJoCo + drivers + calibration. That's heavy to install and impossible to embed in docs, chats, workshops, or agent UIs.

These are tiny single-file HTML apps (20–28 KB, no backend) that run in any browser to teach the core loop: **observation → policy → action → simulated step → recording**.

Use them when you need instant intuition. Switch to real tools for real training.

## Why browser playgrounds?

1. **Zero friction:** No conda env, no `mujoco.viewer`, no ROS install. Open a link and drag a target.
2. **Embeddable:** Works in blog posts, docs, workshops, LMS, chat UIs like Hatch, or other agents — places where native viewers can't run.
3. **Teaches the stack:** Includes a responsibility map — what MuJoCo does, what LeRobot does, what your env does, what ROS 2 does later.
4. **Transfer-minded:** Joint naming matches SO-101 where applicable, so concepts map to `LeRobotDataset v3.0` later.

## What's inside

### `playgrounds/so-101-arm-simulator`
- 6-DOF kinematic SO-101 model
- Joint sliders, preset poses, end-effector readout
- In-memory record / replay demo
- Purpose: learn joint space and teleop → dataset → policy flow

### `playgrounds/lerobot-mujoco-playground`
- **Current state:** Illustrative kinematic 2-link model (Canvas2D, ~28 KB single-file), clearly labeled in UI: *"Illustrative kinematic model — not MuJoCo"*
  - Sliders q0/q1/q2, draggable target, Record / Reset / Run scripted IK / Replay, 90-frame buffer, live EE / TARGET / ERROR / STEP / REWARD
  - Sections: 01 Playground, 02 Control loop, 03 Stack map, 04 Local setup with copyable `pip install mujoco lerobot` commands
  - No external JS deps, only Google Fonts
- **Path to real MuJoCo:** Documents the local next step: real MJCF scene (`assets/tabletop_reach.xml`), Gym env (`src/env.py`), `teleop.py`, `record_episode.py`, `evaluate.py` — not yet in browser bundle

Both are educational — no physics, contacts, gravity, or dataset export yet. That's intentional for teaching.

## When to use this vs real tools

**Use these when:**
- Teaching or onboarding to Physical AI concepts
- You need a demo that runs in a browser, docs, or agent UI
- You want to show the 5-part loop quickly

**Use real tools when:**
- Training real policies: `lerobot-record`, `lerobot-train`, `mujoco.viewer`
- ROS 2 integration: `so101-ros2`, `andino_gz`
- Dataset inspection: `lerobot-dataset-visualizer`, Rerun

## Related work (not novel)

These playgrounds are convenience wrappers. Similar open-source work exists and should be credited:

- [so101-policy-lab](https://github.com/noah-wardlow/so101-policy-lab) — browser SO-101 with MuJoCo WASM + ACT
- [lerobot-playground-portfolio](https://github.com/mefiezvous/lerobot-playground-portfolio) — LeRobot + MuJoCo portfolio
- [lerobot_robot_so101_mujoco](https://github.com/sinfoniauniandes/lerobot_robot_so101_mujoco) — SO-101 MuJoCo as LeRobot hardware
- [vr-teleop-kit](https://github.com/maxidl/vr-teleop-kit) — WebXR teleop + MuJoCo IK
- [lerobot-dataset-visualizer](https://github.com/huggingface/lerobot-dataset-visualizer) — dataset + URDF viewer

Public novelty should come from infrastructure: black-box logging (MCAP + Foxglove), failure-aware kitting, portable skill capture.

## Local setup for real MuJoCo + LeRobot

```bash
uv venv --python 3.11
source .venv/bin/activate
uv pip install mujoco==3.1.6 lerobot

python -c "import mujoco; print(mujoco.__version__)"
python -m mujoco.viewer  # loads assets/tabletop_reach.xml when you add it
```

## Structure

```
browser-robot-playgrounds/
├── playgrounds/
│   ├── so-101-arm-simulator/        # 20 KB single-file kinematic
│   └── lerobot-mujoco-playground/   # 28 KB illustrative kinematic
├── docs/
│   └── WHY_CUSTOM_UI.md
├── LICENSE
└── README.md
```

## License

MIT — educational, no warranty. Credit upstream MJCF / URDF when reusing.

Built Aug 2026 for Physical AI learning.
