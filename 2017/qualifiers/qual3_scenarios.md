# Details of the scenarios used in the third qualification task

This page details the specifics of the scenarios that are used in [the third ARIAC qualification task](https://bitbucket.org/osrf/ariac/wiki/2017/qualifiers/qual3).

Participants are to keep in mind that during the competition they will be presented with previously unseen scenarios and their software must be able to adapt appropriately.

## Part A

The scenario for Part A has the following characteristics:

-   Teams will only be required to be retrieve parts from the stationary bins. The conveyor belt is not used.
-   There are two orders of one kit each:
    - The second order will be announced part-way into the completion of the first order.
    - Kits from both orders can be submitted after this time, but the second order is higher priority and for maximum points it should be completed as fast as possible.
    - To complete the second order, teams can choose to remove the parts already in the kit tray(s), switch to an available empty tray, or submit the first order partially complete to receive an empty tray when the AGV returns.
    - After the second order is complete, the first order is to be resumed.
-   Faulty parts should not be used to build the kits. See [this page](http://wiki.ros.org/ariac/Tutorials/GEARInterface#Faulty_parts) for details on working with faulty parts.

## Part B

The scenario for Part B has the following characteristics:

-   There are two orders of one kit each:
    - The second order will be announced part-way into the completion of the first order.
    - Kits from both orders can be submitted from this time, but the second order is higher priority and for maximum points it should be completed as fast as possible.
    -   Teams can choose to re-purpose the parts in the tray for the new order if appropriate.
    -   After the second order is complete, the first order is to be resumed.
- The second order contains parts that must be flipped. See [this page](https://bitbucket.org/osrf/ariac/wiki/2017/frame_specifications#markdown-header-flipped-parts) for details on working with flipped parts.
-   Faulty parts should not be used to build the kits. See [this page](http://wiki.ros.org/ariac/Tutorials/GEARInterface#Faulty_parts) for details on working with faulty parts.
-   The conveyor belt is used.
    - Both orders include parts that are available in the bins and/or on the conveyor belt.
    - Ten of the "conveyor belt parts" will pass along the conveyor belt. The parts will be disposed of once they reach the end of the conveyor belt if they are not otherwise removed by the robot arm.
    - The conveyor belt is allowed to be controlled for this qualification task (see [these instructions](http://wiki.ros.org/ariac/Tutorials/GEARInterface#Controlling_the_conveyor_belt)). The use of any other 'cheat' interfaces is not permitted during the submission of this qualification task.
