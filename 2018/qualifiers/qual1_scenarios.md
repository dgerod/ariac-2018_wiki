# Details of the scenarios used in the first qualification task

This page details the specifics of the scenarios that are used in [the first ARIAC 2018 qualification task](https://bitbucket.org/osrf/ariac/wiki/2018/qualifiers/qual1).

The following applies to both scenarios:

- The use of any 'cheat' interfaces is not permitted and will be blocked in the automated evaluation setup.
- The trials have a time limit of 500 seconds. Any unsubmitted shipments when the time limit has elapsed will not be scored.
- Simulation state logging will be enabled via the `gazebo_state_logging: true` setting in the the trial config file, [like this](https://bitbucket.org/osrf/ariac/src/4949e714932794b40513f6660d1af119148e2d67/osrf_gear/config/quals/qual1a.yaml?fileviewer=file-view-default#qual1a.yaml-20).

## Part A

Part A is released for teams to practice with. It can be run with the following command, being sure to specify your team's environment configuration file:

```
rosrun osrf_gear gear.py -f `catkin_find --share --first-only osrf_gear`/config/quals/qual1a.yaml <path_to_your_config_file>.yaml
```

The scenario for Part A has the following characteristics:

- There are two orders of one shipment each:
    - The second order will be announced part-way into the completion of the first order.
    - Shipments from both orders can be submitted after this time, but the second order is higher priority and for maximum points it should be completed as fast as possible.
    - The second order does not have a time limit, but should be completed as fast as possible.
    - To complete the second order, teams can choose to remove the products already in the shipping box(es) or switch to an empty shipping box.
    - After the second order is complete, the first order is to be resumed.
-   Faulty parts should not be used to build the fulfill the orders. See [this page](http://wiki.ros.org/ariac/2018/Tutorials/GEARInterface#Faulty_products) for details on working with faulty products.
- The second order contains products that must be flipped. See [this page](https://bitbucket.org/osrf/ariac/wiki/2018/frame_specifications#markdown-header-flipped-products) for details on working with flipped parts.

## Part B

Part B is not released for teams to practice with. In Part B teams will be presented with a previously unseen scenario and their software must be able to adapt appropriately.

The scenario for Part B has the following characteristics:

- All agility challenges released at 5 March 2018 may be present:
    - Faulty products.
    - High-priority order interruption.
    - Flipped products (only the `pulley_part` product can be flipped).
    - Insufficiently many non-faulty products available for order completion.
- There will be at most two orders, each made up of at most 2 shipments.
- The same 5 storage bins used in Part A will be positioned in the environment.
    - Some storage bins may be empty.
    - There will be at most one type of product per bin.
- Users do not have control over the positioning of the quality control sensors, they will be in the same location as for Part A.
- The following product types may be used in the order(s): `gear_part`, `piston_rod_part`, `pulley_part`, `gasket_part`, and `disk_part`.
    - Logical cameras will refer to model types by these names. They will also report `shipping_box` models.
    - Pulleys are the only products that can be requested to be flipped.
    - All products will start in the storage bins un-flipped.