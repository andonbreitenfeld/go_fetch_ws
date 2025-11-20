# go_fetch_ws
CLA Course Project

This repository is a complete ROS 2 workspace for the "Go Fetch!" demo on NRG's B3V0 robot platform.

For this demo, Spot will navigate between predefined waypoints, autonomously grasp balls, and deposit them into a designated collection bin.  

Custom repositories inside src:
- spot_tennis_demo -> object localization & navigation  
- spot_arm_control -> manipulation  
- tennis_demo_behaviorized -> behavior tree (BT)

## Requirements
It is intended to run on a shared robot environment where all required ROS 2 and system dependencies are already installed.  

It is expected that the AprilTag-tagged blue bin is visible to Spot’s left-side camera after undocking, and that no obstacles are blocking the waypoints next to the glovebox.

Additionally, the user must have access to the Docker daemon on the B3V0 machine.

## Clone

`git clone --recursive git@github.com:andonbreitenfeld/go_fetch_ws.git`
`cd go_fetch_ws`

If you forgot to clone recursively:

`git submodule update --init --recursive`

## Build

`colcon build`
`source install/setup.bash`

## Environment Variable

Before running the demo, ensure the following variable is added to your bashrc:

`echo 'export SPOT_ACCESSORIES="ARM RL_KIT"' >> ~/.bashrc`
`source ~/.bashrc`

## Running Demo

Currently the demo is split into 2 unintegrated parts: single task autonomous manipulation and continous surveying. Future efforts will be made to combine into 1 cohesive demo (ie behavior tree doesn't include manipulation yet).

### Part 1: Surveying Using a Behavior Tree

To launch the autonomous surveying workflow, open **5 separate terminals** and run:

`ros2 launch spot_tennis_demo demo_bringup.launch.py`

`ros2 launch spot_navigation bringup_launch.py`

`cd src/spot_tennis_demo/docker`

`docker compose up yolo`

`ros2 launch spot_tennis_demo decision.launch.py`

`ros2 run tennis_demo_behaviorized run_tennis_tree`


### Part 2: Single Task Manipulation

To launch the autonomous manipulation workflow, open **5 separate terminals** and run:

`ros2 launch spot_tennis_demo demo_bringup.launch.py`

`ros2 launch spot_navigation bringup_launch.py`

`cd src/spot_tennis_demo/docker`

`docker compose up yolo`

`ros2 launch spot_tennis_demo decision.launch.py`

`Clara stuff`
