This page outlines the specifications for [the Agile Robotics for Industrial Automation Competition](https://www.nist.gov/el/intelligent-systems-division-73500/agile-robotics-industrial-automation) (ARIAC).

The following terminology is frequently used in this document

1. Order: A list of parts and their goal location on a tray.
1. Part: One element of an order.
1. Tray: A surface that hold parts.
1. Kit: A tray and set of parts that make up an order.


# Competition Scenarios

ARIAC requires participants to complete a series of tests centered in an industrial scenario that are based around building kits made up of particular parts. The robot system will work within the environment specified in the Work Environment section.

There are three different test scenarios that all involve moving parts from a supply location to a tray. The possible supply locations are a conveyor belt, and stationary bins. Challenges will be introduced in each scenario. Details about the scenarios follow.

1. **Scenario 1: Baseline Kit Building**

    The first scenario is intended as a baseline set of tasks for the other test methods to be compared against. The task for this scenario is to pick specific parts and place them on a tray. The robot arm will receive an *Order* that details the list of parts and their target locations. Orders are covered in more detail in the Orders section.

2. **Scenario 2: Dropped Part**

    The task for scenario 2 is identical to scenario 1, however one or more parts will drop from the robot's gripper. The robot will need to recover after dropping a part and complete the given Order. Recovery could entail picking up the dropped part, or fetching a new part.

3. **Scenario 3: In-Process Kit Change**

    While the robot is in the middle of assembling a kit, a new high priority order will be received that needs to be completed as fast as possible. The robot will need to decide how best to complete this new order, and then complete the previous order.

The competition will consist of 15 trials: 5 trials of each of the 3 scenarios. Each trial will receive a score based on completion and efficiency metrics outlined in the Scoring section.

# Environment

The simulation environment is a representation of an industrial kitting work cell with a robot arm, conveyor belt, part bins, and trays.

![ARIAC_full.png](https://bitbucket.org/repo/pB4bBb/images/1577073220-ARIAC_full.png)

The conveyor belt is a **1 m wide** plane that transports objects across the work environment at a fixed speed of roughly **0.2 m/s**. Parts continuously appear on the belt for the duration of the a trial. When parts reach the end of the conveyor belt they are automatically removed. Teams can control the conveyor belt during development, but not during the final competition.

There are eight part bins that may be used for building kits. Parts in these bins will not be replaced once used.

There is a robot arm mounted on a linear actuator that operates parallel to the conveyor belt. The linear actuator measures **4 m**.

Two automated guided vehicles (AGV) are located at either end of the linear actuator. Kits are built on top of these AGVs. A team will programmatically signal the AGVs when the kits are ready to be taken away. The signaled AGV will depart for a short period and then return with an empty tray.

The trays used for assembling kits are flat trays measuring **0.5 x 0.7 m**.

# Robot Arm

The robot arm used in each trial will be a Universal Robots UR10.

The robot arm's position is controlled through the linear actuator on which it is mounted.

The end of the arm is equipped with a vacuum gripper. The vacuum gripper is controlled in a binary manner and reports whether or not it is successfully gripping an object.

# Sensors

A team can place sensors around the environment. Each sensor has a cost that factors into the final score.

Available sensors are:

1. Break beam: reports when a beam is broken by an object. It does not provide distance information.
1. Laser scanner: provides an array of distances to a sensed object.
1. Cognex logical camera: provides information about the pose and type of all models within its field of view.
1. Proximity: detects the range to an object.

For the details about the costs of the sensors see the Costs section. For the details about how to configure the sensor locations, see the [Configuration Specifications](https://bitbucket.org/osrf/ariac/wiki/2017/configuration_spec).

# Order
An order is an instruction containing kits for the robot system to complete.

Each order will specify the kit to be assembled, i.e. the list of parts to be put in the kit.

Each specified part has the following structure:

1. The type of part.
1. The position and orientation of the part on the tray.

For more details see [the part specification](https://bitbucket.org/osrf/ariac/wiki/2017/frame_specifications) page.

# Faulty parts

Above each AGV is a quality control sensor that detects faulty parts.
If faulty parts are detected while teams are filling trays, those parts should be removed from the tray and replaced with another part of the same type.
Faulty parts are considered unwanted parts: they will not count for any points when the kit is submitted, and they will cost teams the all-parts bonus if left in trays (see Scoring, below).

# Scoring

Scores will be automatically calculated for each trial as a combination of performance metrics and costs.
See [the scoring specification](https://bitbucket.org/osrf/ariac/wiki/2017/scoring) page for full details.

# Competition process

Each trial will consist of the following steps:

1. The robot programmatically signals that it is able to begin accepting orders.

1. The first Order (Order 1) is sent to the robot.

1. A fixed amount of time is allowed to complete the order.

1. In the case of the Dropped Part testing method, up to three parts will be forcibly dropped from the gripper.

1. In the case of the In-Process Kit Change testing method, a new Order (Order 2) will be issued that is of higher priority than the previously issued Order 1. When Order 2 is complete, building of Order 1 is to resume.

1. The robot signals programmatically when a kit is complete and ready for quality control.

1. The robot system will be notified that the trial is over. The trial is over when time runs out or all Orders have been fulfilled.

For details on how the communication with the competition system is performed during the trial, see the [Competition Interface](https://bitbucket.org/osrf/ariac/wiki/2017/competition_interface_documentation).
