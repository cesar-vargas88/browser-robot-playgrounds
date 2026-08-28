# Why browser playgrounds? Is this novel?
Short answer: **no** — it's a teaching convenience.

## The reality
- MuJoCo has an official WASM demo.
- LeRobot has Rerun + `lerobot-dataset-visualizer` for datasets and 3D replay.
- There are at least 4 public SO-101 browser labs with MuJoCo WASM + policies:
  - so101-policy-lab (browser ACT + MolmoAct2)
  - lerobot-playground-portfolio (MuJoCo Playground + ACT/Diffusion)
  - lerobot_robot_so101_mujoco (LeRobot hardware plugin)
  - vr-teleop-kit (WebXR + MuJoCo IK)
If you publish another generic viewer claiming novelty, reviewers will point to those.

## So why build browser versions?
1. **Real stack is heavy:** Python + MuJoCo + drivers + calibration takes time to install. Not every team can do it quickly.
2. **Zero-install learning:** Drag a target, move joints, see telemetry, record/replay, and understand the stack without setup.
3. **Embeddable:** Works anywhere a browser works — docs, LMS, Hatch chat, other agents, workshops.
4. **Teaching the stack:** Includes a responsibility map — what MuJoCo does, what LeRobot does, what you do.

## What these are NOT
- Not MuJoCo physics (current bundle is kinematic, labeled as such)
- Not a LeRobotDataset exporter (in-memory buffer only, 90 frames)
- Not a replacement for real training

## When to use real tools
For real policy training or client work, use upstream directly:
- `python -m mujoco.viewer`
- `lerobot-record`, `lerobot-train`, `lerobot-dataset-viz`
- `so101-ros2` + `andino_gz` for ROS 2

Your public credibility won't come from another viewer. It comes from:
- Black-box logging with MCAP + Foxglove + Rust
- Failure-aware kitting cell
- Portable expert-skill capture

Keep the playgrounds as educational wrappers, clearly credited, and focus novelty claims on the infrastructure that makes them useful.
