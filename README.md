# go_fetch_ws
CLA Course Project

This repository is a complete ROS 2 workspace for the "Go Fetch!" demo on NRG's B3V0 robot platform.

For this demo, Spot will navigate between predefined waypoints, autonomously detect and grasp tennis balls, and deposit them into a designated AprilTag-marked collection bin.

The full integrated demo combines autonomous navigation, ball detection, approach planning, and manipulation into a single behavior tree workflow.

## Repository Structure

Custom repositories inside `src/`:
- **spot_tennis_demo** → Launch files, YOLO detection, and perception pipeline
- **tennis_demo_behaviorized** → Behavior tree logic, navigation decisions, and manipulation sequencing

## Requirements

- Intended to run on B3V0 shared robot environment
- User must have access to the Docker daemon on the B3V0 machine
- AprilTag-tagged bin must be visible to Spot's left after undocking (can be changed by editing Waypoint A)
- Waypoints B & C must be obstacle-free (set near the Glovebox)

## Clone

```bash
git clone --recursive git@github.com:andonbreitenfeld/go_fetch_ws.git
cd go_fetch_ws
```

If you forgot to clone recursively:
```bash
git submodule update --init --recursive
```

## Build

```bash
colcon build
source install/setup.bash
```

## Environment Variable

Before running the demo, ensure the following variable is added to your bashrc:

```bash
echo 'export SPOT_ACCESSORIES="ARM RL_KIT"' >> ~/.bashrc
source ~/.bashrc
```

### Launch Sequence

Open **5 separate terminals** and run the following commands in order:

#### Terminal 1: Spot Drivers & Core Systems
```bash
ros2 launch spot_tennis_demo demo_bringup.launch.py
```

#### Terminal 2: Navigation Stack
```bash
ros2 launch spot_navigation bringup_launch.py
```

### ADD MOVE GROUP STUFF CLARA PLEASE

#### Terminal 3: YOLO Detection (Docker)
```bash
cd src/spot_tennis_demo/docker
docker compose up yolo
```

#### Terminal 4: Perception Pipeline
```bash
ros2 launch spot_tennis_demo perception.launch.py
```

#### Terminal 5: Behavior Tree
```bash
ros2 run tennis_demo_behaviorized run_tennis_tree
```

### What Happens

1. **Startup**: Spot claims, powers on, undocks, and navigates to startup position
2. **Bin Localization**: Continuously attempts to locate the AprilTag bin until successful
3. **Patrol & Monitor**: Cycles between waypoints while monitoring for stable ball detections
4. **Fetch Sequence**: Upon detecting a ball:
   - Computes approach goal and navigates to it
   - Executes grasp sequence
   - Returns to bin and deposits ball
5. **Resume Patrol**: Returns to waypoint cycling until next ball is detected

### System Architecture

- **Perception**: YOLO 3D detections → Custom BallSelector filter node → Stable Ball Pose
- **Planning**: Custom ComputeApproachGoal behaviors for ball & bin
- **Navigation**: Used premade WalkToPose behavior for precise positioning
- **Manipulation**: Custom PickBall and DropBall behaviors

## License

MIT

## Authors

- Andon Breitenfeld
- Clara Summerford
- Luke Pronga
