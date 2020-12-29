# Details of the scenarios used in the second qualification task

This page details the specifics of the scenarios that are used in [the second and final ARIAC 2018 qualification task](https://bitbucket.org/osrf/ariac/wiki/2018/qualifiers/qual2).

The following applies to both scenarios:

- The trials have a time limit of 500 simulation seconds. Any unsubmitted shipments when the time limit has elapsed will not be scored. Subscribe to the `/clock` topic to know the current simulation time.
- The use of any 'cheat' interfaces is not permitted and will be blocked in the automated evaluation setup.
- The automated evaluation setup will also prevent sensors from resuming data publishing during the sensor blackout period if subscribers connect to them.

## Part A

Part A is released for teams to practice with. It can be run with the following command, being sure to specify your team's environment configuration file:

```
rosrun osrf_gear gear.py -f `catkin_find --share --first-only osrf_gear`/config/quals/qual2a.yaml <path_to_your_config_file>.yaml
```

By default simulation state logging is enabled in the trial config file. To disable it during development you can add `--state-logging=no` to the above invocation.

The scenario for Part A has the following characteristics:

- There is one order of two shipments.
- The order will be updated while it is being fulfilled.
    - Shipments will be evaluated against the updated order.
    - Teams should respond by filling the updated order instead of the original order.
- The gripper will become faulty at various instances:
    - A disk_part will be dropped in the storage bin.
    - A gasket_part will be dropped in the shipping box.
- Communication with the sensors will be lost for 30 simulation seconds.
    - Teams should continue to fill the order as usual during this time.


## Part B

Part B is not released for teams to practice with. In Part B teams will be presented with a previously unseen scenario and their software must be able to adapt appropriately.

The scenario for Part B has the following characteristics:

- All agility challenges released at 2 April 2018 may be present (see [this page](https://bitbucket.org/osrf/ariac/wiki/2018/agility_challenges) for challenge descriptions):
    - Faulty products.
    - High-priority order interruption.
    - Flipped products (only the `pulley_part` product can be flipped).
    - Insufficiently many non-faulty products available for order completion.
    - Updates to an existing order.
    - Faulty gripper leading to dropped products.
    - Lost sensor communication leading to sensor blackout.
- There will be at most two orders, each made up of at most 2 shipments.
- The same 5 storage bins used in Part A will be positioned in the environment.
    - Some storage bins may be empty.
    - There will be at most one type of product per bin.
- Users do not have control over the positioning of the quality control sensors, they will be in the same location as for Part A.
- The following product types may be used in the order(s): `gear_part`, `piston_rod_part`, `pulley_part`, `gasket_part`, and `disk_part`.
    - Logical cameras will refer to model types by these names. They will also report `shipping_box` models.
    - Pulleys are the only products that can be requested to be flipped.
    - All products will start in the storage bins un-flipped.