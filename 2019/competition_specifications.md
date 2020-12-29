This page outlines the specifications for [the Agile Robotics for Industrial Automation Competition](https://www.nist.gov/el/intelligent-systems-division-73500/agile-robotics-industrial-automation) (ARIAC) 2019.

The following terminology is frequently used in this document:

1. Order: A set of shipments.
1. Product: One element of an order.
1. Tray: A surface that hold products.
1. Kit: A tray and set of products that make up an order.


# Competition Scenarios

ARIAC requires participants to complete a series of tests centered in an industrial scenario that are based around order fulfillment. The robot system will work within the environment specified in the Work Environment section.

There are three different test scenarios that all involve moving products from a supply location to a shipping box. The possible supply locations are a set of stationary bins. Challenges will be introduced in each scenario. Details about the scenarios follow.

1. **Scenario 1: Baseline Kit Building**

    The first scenario is intended as a baseline set of tasks for the other test methods to be compared against. The task for this scenario is to pick specific products and place them on a tray. The robot system will receive an *Order* that details the list of products and their target locations. Orders are covered in more detail in the Orders section.

2. **Scenario 2: Dropped Product**

    The task for scenario 2 is identical to scenario 1, however one or more products will drop from the robot's gripper. The robot will need to recover after dropping a product and complete the given Order. Recovery could entail picking up the dropped product, or fetching a new product.

3. **Scenario 3: In-Process Order Change**

    While the robot is in the middle of assembling a kit, a new high priority order will be received that needs to be completed as fast as possible. The robot will need to decide how best to complete this new order, and then complete the previous order.

The competition will consist of 15 trials: 5 trials of each of the 3 scenarios. Each trial will receive a score based on completion and efficiency metrics outlined in the Scoring section.

Details of the agility challenges used in these scenarios can be found on the [Agility Challenge](https://bitbucket.org/osrf/ariac/wiki/2019/agility_challenges) page.

# Environment

The simulation environment is a representation of an order fulfillment workcell with two robot arms, a conveyor belt, product bins, and trays.

![![ariac_2019.jpg](https://todo/shane/annotated-environment-picture](https://bitbucket.org/repo/pB4bBb/images/3336948939-ariac_overview_labeled.png))

The conveyor belt is a **0.65 m wide** plane that transports objects across the work environment.

The following properties impact teams' interaction with the belt:

1. Products will travel down the belt at a fixed speed of **0.2 m/s**.
1. Teams can control the conveyor belt during development, but not during the final competition.
1. There is a limited supply of products on the belt, and any products placed on the belt are automatically removed if they reach the end of the belt. Products will not be replaced once removed.

There are six product bins that may be used for building kits. Products in these bins will not be replaced once used. 
All products in a particular storage bin are of the same type and have the same orientation.
The product bins are shallow boxes measuring **0.6 x 0.6 m**. 

Orders must be placed on a tray at one of two AGVs.
Teams programmatically signal the AGVs when a kit is ready to be delivered.
The tray is shallow and measures **0.5 x 0.7 m**

There are two robot arms mounted on a linear actuator that operates parallel to the conveyor belt.
The linear actuator measures **4.6 m**, but the travel of each arm is limited to **2.76 m**.
A single arm can reach one AGV and four of the six product bins.


# Robot Arms

Two robot arms will be in the environment for each trial.
The arm used is a Universal Robots UR10.

The robot arm's position is controlled through the linear actuator on which it is mounted.

The end of the arm is equipped with a vacuum gripper. The vacuum gripper is controlled in a binary manner and reports whether or not it is successfully gripping an object.

# Sensors

Teams can place sensors around the environment in static locations. Each sensor has a cost that factors into the final score.

Available sensors are:

1. Break beam: reports when a beam is broken by an object. It does not provide distance information.
1. Laser scanner: provides an array of distances to a sensed object.
1. Depth camera: provides a point cloud of sensed distances.
1. Cognex logical camera: provides information about the pose and type of all models within its field of 
view.
1. Proximity: detects the range to an object.

Sensors can be placed in any free space in the workcell, they do not need to be mounted so that they are touching the conveyor belt/support frame of the storage bin.
Sensors must be used in a realistic manner and must not exploit any simulation technicalities such as the logical camera seeing through obstructions.

For the details about how to configure the sensor locations, see the [Configuration Specifications](https://bitbucket.org/osrf/ariac/wiki/2019/configuration_spec).

# Order
An order is an instruction containing kits for the robot system to complete.

Each order will specify the list of products to be put in the shipment, including the type and position/orientation of each product.
An order may require being delivered to a particular AGV.

For more details see [the product specification](https://bitbucket.org/osrf/ariac/wiki/2019/frame_specifications) page.

# Faulty products

Throughout the workcell are quality control sensors that detect faulty products.
If faulty products are detected while teams are fulfilling orders, those products should be removed from the tray and replaced with another product of the same type.
Faulty products will not count for any points when the shipment is submitted, and they will cost teams the all-products bonus if left in trays (see Scoring, below).

# Scoring

Performance scores will be automatically calculated for each trial as a combination of performance metrics and costs.
These will be combined with scores from judges to determine the final winners.
See [the Scoring Metrics page](https://bitbucket.org/osrf/ariac/wiki/2019/scoring) for more details.

# Competition process

Each trial will consist of the following steps:

1. The robot programmatically signals that it is able to begin accepting orders.

1. The first Order (Order 1) is sent to the robot.

1. A fixed amount of time is allowed to complete the order.

1. In the case of the Dropped Product testing method, up to three products will be forcibly dropped from the gripper.

1. In the case of the In-Process Order Change testing method, a new Order (Order 2) will be issued that is of higher priority than the previously issued Order 1. When Order 2 is complete, building of Order 1 is to resume.

1. The robot signals programmatically when a kit is complete and ready to be delivered.

1. The robot system will be notified that the trial is over. The trial is over when time runs out or all Orders have been fulfilled.

For details on how the communication with the competition system is performed during the trial, see the [Competition Interface](https://bitbucket.org/osrf/ariac/wiki/2019/competition_interface_documentation).

There are no time limits for individual orders, but each trial has a time limit.
This information is not broadcast by the ARIAC server.
For the Finals/Qualifiers, the time limit will be set as a fixed value for all trials, which teams will be advised of in advance.