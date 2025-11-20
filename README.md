# go_fetch_ws
CLA Course Project

This repository is a complete ROS 2 workspace for the "Go Fetch!" demo on NRG's B3V0 robot platform.

It is intended to run on a shared robot environment where all required ROS 2 and system dependencies are already installed.  

For this demo, Spot will navigate between predefined waypoints, autonomously grasp balls, and deposit them into a designated collection bin.  

It is expected that the AprilTag-tagged blue bin is visible to Spot’s left-side camera after undocking, and that no obstacles are blocking the waypoints next to the glovebox.

Additionally, the user must have access to the Docker daemon on the B3V0 machine.

## Clone

git clone --recursive git@github.com:andonbreitenfeld/go_fetch_ws.git  
cd go_fetch_ws

If you forgot to clone recursively:

git submodule update --init --recursive

## Build

colcon build  
source install/setup.bash

You must run **colcon build** after cloning the repository for the demo to function correctly.
