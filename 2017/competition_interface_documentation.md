# ARIAC Interface

GEAR provides a [ROS](http://www.ros.org/) interface to the teams participating in ARIAC. This interface can be used by teams to control all available actuators, read sensor information and send/receive notifications.

During the competition, it is against the rules to control the ARIAC simulation using anything other than the interface specified below. **Teams are not permitted to use any of the topics or services in the `/gazebo/` namespace prefix to control the Gazebo simulation or get information about the simulation state. These interfaces will be blocked during the Finals.**

For a hands-on tutorial on interfacing with GEAR through command line tools, see [the Gear Interface tutorial](http://wiki.ros.org/ariac/Tutorials/GEARInterface). For a tutorial on interfacing with GEAR through a ROS node, see the [Hello World tutorial](http://wiki.ros.org/ariac/Tutorials/HelloWorld).


## Sensors

|Topic name|Message/Service|Description|Message definition|
|----------|-----------|------------------|---------------|
|/ariac/{name}  | Message|  Break beam's output    |  [osrf_gear/Proximity.msg](https://bitbucket.org/osrf/ariac/raw/ariac_2017/osrf_gear/msg/Proximity.msg)  |
|/ariac/{name}_change  | Message|  Break beam's output (output changes only)    |  [osrf_gear/Proximity.msg](https://bitbucket.org/osrf/ariac/raw/ariac_2017/osrf_gear/msg/Proximity.msg)  |
|/ariac/{name}  | Message|  Proximity sensor's output    |  [sensor_msgs/Range.msg](http://docs.ros.org/api/sensor_msgs/html/msg/Range.html)  |
|/ariac/{name}  | Message|  Laser profiler's output    |  [sensor_msgs/LaserScan.msg](http://docs.ros.org/api/sensor_msgs/html/msg/LaserScan.html)  |
|/ariac/{name}  | Message|  Logical camera's output    |  [osrf_gear/LogicalCameraImage.msg](https://bitbucket.org/osrf/ariac/raw/ariac_2017/osrf_gear/msg/LogicalCameraImage.msg)  |


Note: The string `{name}` is replaced with the name you give the sensor in the config file. See: https://bitbucket.org/osrf/ariac/wiki/2017/configuration_spec Since the sensor names are unique, it ensures that all sensors publish data to unique topics.


## TF frames
TF frames for static key points of the workcell are published by the ARIAC simulation.
Dynamic TF frames for the arm and faulty parts are also published by the simulation. Other dynamic TF frames can be accessed through logical cameras.

|Description|TF frame|Type|
|----------|-----------|---|
| Origin of the work cell | world | static |
| Each sensor | `{sensor_name}_frame`, e.g. logical_camera_1_frame | static |
| Bin storage units | `bin{N}_frame`, where N=1..8 | static |
| AGV load points | `agv{N}_load_point_frame`, where N=1..2 | static |
| Arm links | `{link_name}`, e.g. wrist1_link | dynamic |
| Parts detected by logical cameras | `{logical_camera_name}_{part_name}_frame`, e.g. logical_camera_1_piston_rod_part_1_frame | dynamic |
| Parts detected by quality control sensors | `quality_control_sensor_{N}_{part_name}_frame`, where N=1..2, e.g. quality_control_sensor_1_piston_rod_part_1_frame | dynamic |
| Kit trays detected by logical cameras | `{logical_camera_name}_kit_tray_{N}_frame`, where N>0, e.g. logical_camera_1_kit_tray_1_frame | dynamic |
| Actual AGV pose detected by logical cameras | `{logical_camera_name}_agv{N}_frame`, where N=1..2, e.g. logical_camera_1_agv1_frame | dynamic |


## Actuators

|Topic name|Message/Service|Description|Message definition|
|----------|-----------|------------------|---------------|
|/ariac/arm/command  |   Message    | Update the arm | [trajectory_msgs/JointTrajectory.msg](http://docs.ros.org/api/trajectory_msgs/html/msg/JointTrajectory.html)
|/ariac/joint_states  |   Message    | Arm joint states | [sensor_msgs/JointState](http://docs.ros.org/api/sensor_msgs/html/msg/JointState.html)
|/ariac/arm/state  |   Message    | Arm Controller's state | [control_msgs/JointTrajectoryControllerState.msg](http://docs.ros.org/api/control_msgs/html/msg/JointTrajectoryControllerState.html)
|/ariac/gripper/control  |   Service    |  Enable/disable gripper's suction| [osrf_gear/VacuumGripperControl.srv](https://bitbucket.org/osrf/ariac/raw/ariac_2017/osrf_gear/srv/VacuumGripperControl.srv)|
|/ariac/gripper/state  |   Message    | Gripper's state| [osrf_gear/VacuumGripperState.msg](https://bitbucket.org/osrf/ariac/raw/ariac_2017/osrf_gear/msg/VacuumGripperState.msg)|

## Process management

|Topic name                |Message/Service|Description          |Message definition|
|--------------------------|---------------|---------------------|------------------|
|/clock  |Message |[Simulation time](http://wiki.ros.org/Clock#Using_Simulation_Time_from_the_.2BAC8-clock_Topic)      |  [rosgraph_msgs/Clock.msg](http://docs.ros.org/api/rosgraph_msgs/html/msg/Clock.html)       |
|/ariac/start_competition  |Service        |Start the competition|  [std_srvs/Trigger.srv](http://docs.ros.org/api/std_srvs/html/srv/Trigger.html)       |
|/ariac/orders  |   Message     |New order to be completed       |  [osrf_gear/Order.msg](https://bitbucket.org/osrf/ariac/raw/ariac_2017/osrf_gear/msg/Order.msg)|
|/ariac/material_locations  |Service        |Query storage locations for a material (e.g. kit_tray, pulley_part)|  [osrf_gear/GetMaterialLocations.srv](https://bitbucket.org/osrf/ariac/raw/ariac_2017/osrf_gear/srv/GetMaterialLocations.srv)       |
|/ariac/agv{N}  |Service        |Notify AGV{N} that the kit is ready (N=1,2)|  [osrf_gear/AGVControl.srv](https://bitbucket.org/osrf/ariac/raw/ariac_2017/osrf_gear/srv/AGVControl.srv)       |
|/ariac/agv{N}/state  |Message        |State of AGV {N} (N=1,2)|  [std_msgs/String.msg](http://docs.ros.org/api/std_msgs/html/msg/String.html)       |
|/ariac/quality_control_sensor_{N}  | Message|  Output of quality control sensor {N} (N=1,2)    |  [osrf_gear/LogicalCameraImage.msg](https://bitbucket.org/osrf/ariac/raw/ariac_2017/osrf_gear/msg/LogicalCameraImage.msg)  |


## Cheats

These are only provided for debugging/development purposes and their use is not permitted during the competition trials. See [the developer tips page](https://bitbucket.org/osrf/ariac/wiki/2017/developer_tips#markdown-header-running-ariac-with-cheats-enabled) for how to enable cheats.

| Topic name | Message/Service | Description | Message definition |
| ---------- |----------- | ------------------ | --------------- |
| /ariac/conveyor/control  |   Service    |  Modify power of the conveyor belt        | [osrf_gear/ConveyorBeltControl.srv ](https://bitbucket.org/osrf/ariac/raw/ariac_2017/osrf_gear/srv/ConveyorBeltControl.srv)          |
| /ariac/trays  |   Message    | State of the kit being built on each tray        | [osrf_gear/TrayContents.msg ](https://bitbucket.org/osrf/ariac/raw/ariac_2017/osrf_gear/msg/TrayContents.msg)          |
| /ariac/submit_tray  |   Service    |  Submit a tray for evaluation without the AGV moving        | [osrf_gear/SubmitTray.srv ](https://bitbucket.org/osrf/ariac/raw/ariac_2017/osrf_gear/srv/SubmitTray.srv)          |
| /ariac/kit_tray_{N}/clear_tray  |   Service    |  Clear the contents of tray {N} without the AGV moving        | [std_srvs/Trigger.srv ](http://docs.ros.org/api/std_srvs/html/srv/Trigger.html)          |