# Developer tips

This page collates some tips that may be useful for users developing software for ARIAC.

## **Shorter ARIAC teardown time**

When ARIAC is launched, several processes are run, one of which is `gzserver`. This process does not always terminate properly when ARIAC is being torn down, and as a result must be terminated by `roslaunch`. The amount of time that passes before this occurs defaults to more than 15 seconds. To shorten it, edit the `_TIMEOUT_SIGINT` variable at the top of the following file:

```
/opt/ros/kinetic/lib/python2.7/dist-packages/roslaunch/nodeprocess.py
```

Choose a value lower than 15, such as 2. Note that this change is permanent (but reversible) and will impact all processes launched with `roslaunch`, not just ARIAC.

## **Save Gazebo configuration**

If you wish to view the Gazebo GUI in a position/size other than the default, rather than moving/rescaling it each time you run ARIAC, you can save the configuration with File > Save Configuration (from within Gazebo).

## **Running ARIAC with sensor views visualized**

By default, sensor visualization in Gazebo is disabled.
To run ARIAC with sensor views visualization enabled (useful for when you are trying to configure your sensor placement), add the `--visualize-sensor-views` option.

```
$ rosrun osrf_gear gear.py --visualize-sensor-views
```

## **Running ARIAC with cheats enabled**

By default, the `ARIAC_COMPETITION` environment variable is set when running ARIAC, which disables cheats. To run ARIAC with cheats enabled, add the `--development-mode` option (or `-d`).

```
$ rosrun osrf_gear gear.py --development-mode
```

## **Teardown ARIAC upon trial completion**

If you set the `ARIAC_EXIT_ON_COMPLETION` environment variable, the process running an ARIAC trial will exit once the trial ends.

```
$ export ARIAC_EXIT_ON_COMPLETION=1
$ rosrun osrf_gear gear.py
```

This change will persist with the terminal in which the environment variable has been set. To undo it, use:

```
$ unset ARIAC_EXIT_ON_COMPLETION
```

## **Running ARIAC with debugging output**

To run ARIAC with debug output, add the `--verbose` option (or `-v`).

```
$ rosrun osrf_gear gear.py --verbose
```

## **Running ARIAC with simulation state logging enabled**

[Simulation state logs](https://bitbucket.org/osrf/ariac/wiki/2018/logging) can be useful for replaying a simulation for inspection.
By default, simulation state logging is disabled, but it can be enabled with the `--state-logging=true` option.

```
$ rosrun osrf_gear gear.py --state-logging=true
```

## **Running ARIAC without simulation visualization**
To run ARIAC without simulation visualization, add the `--no-gui` option. Simulation state logging (see above) will still work and logs can be played back with visualization afterwards.

```
$ rosrun osrf_gear gear.py --no-gui
```

## **rqt**
The `rqt` GUI has many plugins that are useful for development. The [`Joint trajectory controller`](http://wiki.ros.org/ariac/2018/Tutorials/GEARInterface#rqt_GUI) and the `Service caller` may be of particular use to ARIAC developers.

## **MoveIt**
MoveIt provides an RViz plugin for interacting with the arm. See [the MoveIt ARIAC tutorial](http://wiki.ros.org/ariac/2018/Tutorials/MoveItInterface).

## **Spawning models in the ARIAC environment**
It may be useful for development purposes to spawn models in the ARIAC Gazebo environment. An example of doing so is:

```
rosrun gazebo_ros spawn_model -sdf -file `catkin_find osrf_gear --share --first-only`/models/gear_part_ariac/model.sdf -x 1.192 -y 3.92 -z 0.5 -model gear_part_0
```

Note that in order for models to be detected by the logical cameras, they must following the naming convention of `<model_name>_<N>` e.g. `gear_part_0`.

## **Monitoring TF frames**
Various components of ARIAC publish transform frames, such as a logical camera publishing the poses of the products that it sees.
The `tf` package provides some command-line tools for interacting with transform information. For example, to know the pose of a frame with respect to the ARIAC environment origin, run:

```
$ rosrun tf tf_echo /world /bin3_frame
At time 0.000
- Translation: [-0.300, 0.230, 0.720]
- Rotation: in Quaternion [0.000, 0.000, 0.707, 0.707]
            in RPY (radian) [0.000, -0.000, 1.571]
            in RPY (degree) [0.000, -0.000, 90.000]
```

Note that ARIAC uses `tf2_msgs` and not the deprecated `tf_msgs`. Accordingly, you should use [the `tf2` ROS bindings](http://wiki.ros.org/tf2) instead of `tf`.