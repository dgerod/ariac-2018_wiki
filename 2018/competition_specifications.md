This page outlines the specifications for [the Agile Robotics for Industrial Automation Competition](https://www.nist.gov/el/intelligent-systems-division-73500/agile-robotics-industrial-automation) (ARIAC) 2018.

The following terminology is frequently used in this document:

1. Order: A set of shipments.
1. Shipment: A set of products and their goal location in a shipping box.
1. Product: One element of a shipment.
1. Shipping box: A cardboard box that holds products.


# Competition Scenarios

ARIAC requires participants to complete a series of tests centered in an industrial scenario that are based around order fulfillment. The robot system will work within the environment specified in the Work Environment section.

There are three different test scenarios that all involve moving products from a supply location to a shipping box. The possible supply locations are a set of stationary bins. Challenges will be introduced in each scenario. Details about the scenarios follow.

1. **Scenario 1: Baseline Order Fulfillment**

    The first scenario is intended as a baseline set of tasks for the other test methods to be compared against. The task for this scenario is to pick specific products and place them into a shipping box. The robot system will receive an *Order* that details the list of products and their target locations. Orders are covered in more detail in the Orders section.

2. **Scenario 2: Dropped Product**

    The task for scenario 2 is identical to scenario 1, however one or more products will drop from the robot's gripper. The robot will need to recover after dropping a product and complete the given Order. Recovery could entail picking up the dropped product, or fetching a new product.

3. **Scenario 3: In-Process Order Change**

    While the robot is in the middle of assembling a shipment, a new high priority order will be received that needs to be completed as fast as possible. The robot will need to decide how best to complete this new order, and then complete the previous order.

The competition will consist of 15 trials: 5 trials of each of the 3 scenarios. Each trial will receive a score based on completion and efficiency metrics outlined in the Scoring section.

Details of the agility challenges used in these scenarios can be found on the [Agility Challenge](https://bitbucket.org/osrf/ariac/wiki/2018/agility_challenges) page.
# Environment

The simulation environment is a representation of an order fulfillment workcell with a robot arm, conveyor belt, product bins, and shipping boxes.

![ariac_2018.jpg](http://wiki.ros.org/ariac/2018/Tutorials/GEARInterface?action=AttachFile&do=get&target=annotated_environment.png)

The conveyor belt is a **0.75 m wide** plane that transports objects across the work environment at a variable speed.
The following properties impact teams' interaction with the belt:

1. A limited number of shipping boxes will appear on the belt during a trial, and move through the workcell.
1. Teams can control the power of the conveyor belt, but not its direction.
1. When shipping boxes reach the collection zone at the end of the conveyor belt they are available for collection for delivery.
1. If additional shipping boxes reach the end of the belt while a box is waiting to be collected, the belt will stop to prevent congestion of the collection area. Control of the belt by teams is disabled in this state.
    1. When congestion is no longer detected, control of the belt by teams will be re-enabled. The belt will remain stopped until a power command is received.

There are multiple product bins that may be used for fulfilling orders. Products in these bins will not be replaced once used.
All products in a particular storage bin are of the same type and have the same orientation.

There is a robot arm mounted on a linear actuator that operates parallel to the conveyor belt. The linear actuator measures **4 m**.

Automated delivery drones are located at the end of the conveyor belt.
Shipments are delivered by these drones.
Teams programmatically signal the drones when a shipment is ready to be collected for delivery.
The signaled drone will collect the shipping box and leave to deliver it.

The shipping boxes used for fulfilling orders are shallow boxes measuring **0.5 x 0.7 m**.

# Robot Arm

A robot arm will be in the environment for each trial. At initial release of the ARIAC software the arm used a Universal Robots UR10; it has since been changed to a Kuka IIWA14 with the same ROS interface.

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

For the details about how to configure the sensor locations, see the [Configuration Specifications](https://bitbucket.org/osrf/ariac/wiki/2018/configuration_spec).

# Order
An order is an instruction containing shipments for the robot system to complete.

Each order will specify the list of products to be put in the shipment, including the type and position/orientation of each product.

For more details see [the product specification](https://bitbucket.org/osrf/ariac/wiki/2018/frame_specifications) page.

# Faulty products

Throughout the workcell are quality control sensors that detect faulty products.
If faulty products are detected while teams are fulfilling orders, those products should be removed from the shipping box and replaced with another product of the same type.
Faulty products will not count for any points when the shipment is submitted, and they will cost teams the all-products bonus if left in shipping boxes (see Scoring, below).

# Scoring

Performance scores will be automatically calculated for each trial as a combination of performance metrics and costs.
These will be combined with scores from judges to determine the final winners.
See [the Scoring Metrics page](https://bitbucket.org/osrf/ariac/wiki/2018/scoring) for more details.

# Competition process

Each trial will consist of the following steps:

1. The robot programmatically signals that it is able to begin accepting orders.

1. The first Order (Order 1) is sent to the robot.

1. A fixed amount of time is allowed to complete the order.

1. In the case of the Dropped Product testing method, up to three products will be forcibly dropped from the gripper.

1. In the case of the In-Process Order Change testing method, a new Order (Order 2) will be issued that is of higher priority than the previously issued Order 1. When Order 2 is complete, building of Order 1 is to resume.

1. The robot signals programmatically when a shipment is complete and ready to be delivered.

1. The robot system will be notified that the trial is over. The trial is over when time runs out or all Orders have been fulfilled.

For details on how the communication with the competition system is performed during the trial, see the [Competition Interface](https://bitbucket.org/osrf/ariac/wiki/2018/competition_interface_documentation).

There are no time limits for individual orders, but each trial has a time limit.
This information is not broadcast by the ARIAC server.
For the Finals/Qualifiers, the time limit will be set as a fixed value for all trials, which teams will be advised of in advance.