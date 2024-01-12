# Project: Home Service Robot

## Overview
This project simulates a home service robot capable of autonomous navigation, object transportation, and environment mapping. It integrates various ROS packages to achieve localization, mapping, and navigation functionalities in a Gazebo simulated environment.

## Directory structure


├── add_markers
│   ├── CMakeLists.txt
│   ├── include
│   │   └── add_markers
│   ├── launch
│   │   └── view_add_markers.launch
│   ├── package.xml
│   └── src
│       ├── add_markers.cpp
│       └── add_marker_time_based.cpp
├── map
│   ├── map.pgm
│   └── map.yaml
├── models
│   └── Building
│       ├── model.config
│       └── model.sdf
├── pick_objects
│   ├── CMakeLists.txt
│   ├── include
│   │   └── pick_objects
│   ├── package.xml
│   └── src
│       └── pick_objects.cpp
├── README.md
├── rvizConfig
│   └── home_service_rviz_config.rviz
├── scripts
│   ├── add_markers.sh
│   ├── home_service.sh
│   ├── launch.sh
│   ├── pick_objects.sh
│   ├── test_navigation.sh
│   └── test_slam.sh
└── worlds
    └── SimpleWorld.world

## Key ROS Packages Used

### Localization: `amcl`
The Adaptive Monte Carlo Localization (AMCL) package is crucial for the robot's localization. AMCL dynamically adjusts the number of particles over a period of time, refining the robot's estimated position and orientation. It uses a particle filter to track the pose of a robot against a known map. This package is essential in the `test_navigation.sh` and `pick_objects.sh` scripts for accurate robot positioning within the environment.

### Mapping: `gmapping`
The `gmapping` package provides laser-based SLAM (Simultaneous Localization and Mapping) capabilities. It allows the robot to create a 2D map while navigating an environment. `gmapping` uses a Rao-Blackwellized particle filter to maintain a map. This package is a key component in the `test_slam.sh` script, enabling the TurtleBot to build a map of its surroundings, which is crucial for efficient navigation and localization.

### Navigation: `move_base`
The `move_base` package is a comprehensive solution that integrates global and local planners for the robot to reach a goal. It interacts with `AMCL` or `gmapping` for localization and mapping, and it uses path planning algorithms to navigate the robot to its destination. This package is utilized in the `test_navigation.sh`, `pick_objects.sh`, and `home_service.sh` scripts for directing the robot to specific goals while avoiding obstacles.

## Custom ROS Packages

### `pick_objects`
- **Purpose:** Demonstrates the robot's ability to navigate to specific locations.
- **Functionality:** Utilizes `move_base` to send navigation goals for pickup and dropoff tasks.
- **Key File - `pick_objects.cpp`:** Manages sending sequential goals to the `move_base` action server and logs the robot's status in reaching these goals.

### `add_markers`
- **Purpose:** Simulates object pickup and dropoff visualization.
- **Functionality:** Uses RViz to display markers at designated locations for pickup and dropoff tasks.
- **Key Files:**
  - **`add_marker_time_based.cpp`:** Manages the marker's appearance and disappearance at set time intervals.
  - **`add_markers.cpp`:** Interacts with robot odometry data to dynamically manage marker visualization based on the robot's location.

## Project Steps

### Step 1: SLAM Testing
This step tests the robot's SLAM capabilities using the `gmapping` package. The robot explores the environment and constructs a map using a laser range-finder sensor.

### Step 2: Navigation Testing
This step evaluates the robot's navigation abilities. It uses the `amcl` package for localization and the `move_base` package for path planning and navigation in the known map.

### Step 3: Object Pickup and Dropoff Simulation
Simulating object transportation tasks, this step leverages the `move_base` package to navigate to specific pickup and dropoff points.

### Step 4: Marker Visualization
This step involves visualizing virtual objects as markers in RViz, demonstrating the pickup and dropoff tasks.

### Step 5: Home Service Robot
The final step integrates all functionalities to simulate a home service robot performing autonomous navigation, object transportation, and interaction with virtual markers.

## Conclusion
This project demonstrates a comprehensive application of key ROS packages for autonomous robot navigation in a simulated environment. It encapsulates the practical use of SLAM, localization, and navigation technologies in robotics, along with custom ROS packages for specific task simulations.
