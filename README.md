# PURT Autonomous Fixed-Wing UAV Pylon Racing Competition 2025

**Location:** Purdue UAS Research and Test Facility (PURT)



We are hosting a Purdue internal Pylon racing competition at PURT on April 12, 2025.

Teams will be scored on the fastest laptime around a rectangular course in PURT. The course size will be approximately 50'x50'.

## The Sample Solution Overview

The Python-based controller script is organized as follows:
```
sim_recs_ros_xtrack.py
┗ cross_tracker.py
┗ tecs_xtrack_sample.py
```

The sample solution uses Total Energy Control System (TECS), a cascaded propotional-integral controller, to control the vehicle's airborne states and a form of cross-track minimization navigation algorhm, the sample solution allows autonomous fixed-wing vehicle flights.

The sample solution uses Robot Operating Software (ROS2) with Python interface to perform high-fidelity data processing and computation to control the vehicle at PURT. The gain tuning given in the sample solution provides a guide-line for the general trim for the vehicle.

## Running The Simulator

This sample solution is tested on **Ubuntu 24.04** running **ROS2 Jazzy** version.

First install dependencies and install simulator. This is automatically installed when you install Cognpilot from main branch and recently pulled the "cyecca" branch.

To install the simulator alone in a single workspace:

```
mkdir nvp_ros2_ws/src
cd nvp_ros2_ws/src
git clone https://github.com/CogniPilot/cyecca.git
git clone https://github.com/wsribunma/auav_pylon_2025.git 
cd ..
colcon build --symlink-install
```

Source the workspace
```
source install/setup.bash
```

Running the simulator
```
ros2 launch auav_pylon_2025 fixedwing_sim.xml
```
The launch script should launch a simulation with RVIZ2 visualizer by default.

The real-time simulation can be viewed from RVIZ2 or other ROS2 topic visualizer. 

Current simulation allows an optional use of a joystick controller (Logitech f310). The "A" button will toggle the auto model, and "B" button will toggle the manual mode. To enable joystick commands, add a condition ```use_joystick:=true``` when launching the fixedwing_sim.xml script


## Common Issues
If your simulator doesn't automatically takeoff, it may be that you are on "manual" mode. 
* Fix: go to your "ros2_ws/src/cyecca/scripts/fixedwing_sim.py" and set ```self.input_mode = "auto"```


*Note* By default, the sample solution is set to take off when below a given altitude to force the fixed-wing simulator to take off from the ground.

