Full details of the qual3 task are here: https://bitbucket.org/osrf/ariac/wiki/2017/qualifiers/qual3 but it boils down to these two commands:

```
rosrun osrf_gear gear.py -v -d -f `catkin_find --share osrf_gear`/config/qual3a.yaml `catkin_find --share osrf_gear`/config/sample_user_config.yaml
```
to launch Part A, and

```
rosrun osrf_gear gear.py -v -d -f `catkin_find --share osrf_gear`/config/qual3b.yaml `catkin_find --share osrf_gear`/config/sample_user_config.yaml
```

for Part B.

Consider that step 0. Please read the [scenario descriptions](https://bitbucket.org/osrf/ariac/wiki/2017/qualifiers/qual3_scenarios) to know what is expected after this at a high level. You may find [this page with developer tips](https://bitbucket.org/osrf/ariac/wiki/2017/developer_tips) useful.

## High-level testing

Once the scenario's launched, please do the following:

1. `rosservice call /ariac/start_competition`
1. `rostopic echo /ariac/orders` (should see one order then another later; keep this open in a terminal)
1. Pause the simulation, manually move some parts into one of the trays on the AGV, and resume the simulation. The idea is to move the parts from the order you received in step 2. Don't worry about putting them in the right place.
1. After you put a few parts into the tray another order will come through.
1. Change the tray configuration if you want and submit the tray for scoring with `rosservice call /ariac/agv1 'order_1_kit_0'` (or agv2 if you're building on the AGV on the right). **Check that the AGV doesn't jump around when it comes back from delivery.**
1. The original order is not received on the order topic again, it's just implied that it should resume after the second order is complete.
1. Put some parts in a tray again and submit with
`rosservice call /ariac/agv1 'order_0_kit_0'` (or agv2). **Check that the competition window outputs a final score, and that the times look about right.** The time taken to complete orders is measured from the time originally announced. The score might not be a full score because some parts may have been 'faulty' (see below).


## Additional tasks

Start again and try one of these:

1. Use the arm to pick up a part. See http://wiki.ros.org/ariac/Tutorials/GEARInterface#rqt_GUI to move the arm around; use `rosservice call /ariac/gripper/control true` to enable and disable the gripper.
1. If doing qual3b, try to flip the pulley part. See https://bitbucket.org/osrf/ariac/wiki/2017/frame_specifications#markdown-header-flipped-parts - flipping the part probably requires placing it on its side and then using another grasp to place it on its back.
1. Some parts will be reported as faulty. Use `rostopic echo /ariac/quality_control_sensor_1` to see faulty parts if you're building on the left AGV, otherwise use _2. [These parts](https://bitbucket.org/osrf/ariac/src/75592a713e7e9407bfca849dd65bc4384b011e84/osrf_gear/config/qual3a.yaml?at=ariac_2017&fileviewer=file-view-default#qual3a.yaml-112) should be reported as faulty for qual3a, [these parts](https://bitbucket.org/osrf/ariac/src/75592a713e7e9407bfca849dd65bc4384b011e84/osrf_gear/config/qual3b.yaml?at=ariac_2017&fileviewer=file-view-default#qual3b.yaml-77) for qual3b.
1. Use `rostopic echo /ariac/trays` to see the pose of parts in the tray and try to get a perfect score. Note that this is a 'cheat'.
1. Use `rosrun tf tf_echo /logical_camera_2_kit_tray_1_frame /logical_camera_2_pulley_part_2_frame` or similar to know the pose of parts on the tray and try to get a perfect score (avoid faulty parts).
1. Remove the `-d` option from step 0 and check that `rostopic echo /ariac/trays` makes the competition complain.
1. Check that the second order for qual3a happens when 2 _non-faulty_ parts that _are not_ used in the second order get put onto one of the trays.
1. Check that the second order for qual3b happens when 2 _non-faulty_ parts that _are_ used in the second order get put onto one of the trays.
