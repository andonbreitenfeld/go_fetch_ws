# go_fetch_ws
CLA Course Project

This repository is a complete ROS 2 workspace for the "Go Fetch!" demo on NRG's B3V0 (Boston Dynamics Spot).  
It is intended to run on a shared robot environment where all required ROS2 and system dependencies are already installed.  
Additionally, the user must have access to the Docker daemon on B3V0.

For this demo, Spot will navigate between predefined waypoints, autonomously grasp balls, and deposit them into a designated collection bin.  
It is expected that the AprilTag-tagged blue bin is visible to Spot’s left-side camera after undocking, and that no obstacles are blocking the waypoints placed next to the glovebox.

## Clone

```bash
git clone --recursive git@github.com:andonbreitenfeld/go_fetch_ws.git
cd go_fetch_ws
