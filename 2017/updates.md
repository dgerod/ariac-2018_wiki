# ARIAC competition software news

## **Changes to ARIAC software**
_To determine the version of the ARIAC software that you're running, check the `~/.ariac/log/performance.log` file, which will contain e.g. "ARIAC VERSION: 1.0.3"._
_To update your ARIAC software, run `sudo apt-get update && sudo apt-get install ariac`._

### New in v1.1.4 (2 June 2017, Competition Finals)
1. **Conveyor belt cheat disabled in competition mode.** As explained in the rules, this cheat was only permitted during the qualifiers.

1. **ROS topics and services for interacting directly with the Gazebo simulation blocked.** e.g. `/gazebo/link_states`. As explained in the rules, teams should only interact with ARIAC through the prescribed ROS interface.

1. **Logging directed to file.** Less logging will appear in the console, as more is being directed to ROS log files.

### New in v1.1.2 (13 May 2017)
1. **Improvements to laser profiler.**

    - angular resolution increased from 100 points/scan to 400 points/scan.
    - update rate increased from 20 Hz to 100 Hz.

    If you tested the pre-released change, we suggest that you now remove `/etc/apt/sources.list.d/gazebo-prerelease.list`.


### New in v1.1.1 (Qualification Task 3 release, 17 April 2017)

1.  **Quality control sensors added above each AGV.**

    See http://wiki.ros.org/ariac/Tutorials/GEARInterface#Faulty_parts.

1.  **Parts detected by logical cameras have unique TF frames.**

    TF frames of parts detected by logical cameras/quality control sensors are now prefixed by the name of the sensor. This is to provide unique frames IDs when the same part is seen by multiple cameras. See http://wiki.ros.org/ariac/Tutorials/SensorInterface#Logical_camera for examples.

1.  **Proximity sensor now reports range.**

    The [proximity sensor](http://wiki.ros.org/ariac/Tutorials/SensorInterface#Proximity_sensor) now uses the `sensors_msgs/Range` message type instead of reporting binary values.

1.  **Cheats disabled by default.**

    Running ARIAC software now sets the `ARIAC_COMPETITION` environment variable by default, which disables cheats. To enable cheats, pass `--development-mode` to `gear.py`.

1.  **Logical camera range reduced.**

    The field of view of the logical camera has changed: it has a reduced range and a slightly wider field of view.


### New in v1.0.6 (31 March 2017)
1.  **Sporadic segfault on gripper control fixed.**

### New in v1.0.5 (30 March 2017)
1.  **Kit tray TF frame bug fixed.**

    The issue of logical cameras reporting incorrect TF transforms of kit trays after AGV animations has been resolved. The pose of kit trays published on logical camera output topics with `osrf_gear/LogicalCameraImage` messages is still incorrect -- users are advised to use the TF information.

1.  **Logical cameras now report AGV frames.**

    Logical cameras now detect AGVs in addition to kit trays and parts. The offset between AGV frames and kit tray frames is published as a TF transformation independently of the logical camera.

### New in v1.0.4 (27 March 2017)
1.  **Crash on submission of qual2b fixed.**

    The issue of ARIAC crashing on submission of trays in the qual2b trial has been resolved.

### New in v1.0.3 (24 March 2017)
1.  **Drifting AGV/parts bug fixed.**

    The issue of AGVs/parts on the kit trays slowly drifting in the workcell environment has been resolved.

1.  **AGV state machine modified.**

    A new state in the AGV state machine has been added: `preparing_to_deliver`.

### New in v1.0.2 (15 March 2017)
1.  **Shaking kit tray bug fixed.**

    The issue of kit trays shaking (experienced by users with older versions of the `kit_tray` and `warehouse_robot` models in their ~/.gazebo/models directory) has been resolved.

### New in v1.0.1 (Qualification Task 2 release, 6 March 2017)
1.  **AGV state publishing enabled.**

    The `/ariac/agv{N}/state` topic can be used to obtain information about the state of the AGV.

### New in v1.0.0 (3 March 2017)
1.  **AGV tray delivery enabled.**

    Upon submission requests of trays, AGVs deliver the kit on the tray and return with an empty tray.

1.  **Arm initial configuration removed.**

    Participants are no longer permitted to choose the initial pose of the arm in their configuration file. This is to reflect how controllers are typically developed in manufacturing environments.

1.  **Multiple kits per order enabled.**

    A single order may now contain multiple kits. Participants will have to specify which kit of an order they are submitting when they submit a tray, using the name specified in the order. For example, participants will need to call `rosservice call /ariac/agv1 "kit_type: order_0_tray_0"` instead of `rosservice call /ariac/agv1 "kit_type: order_0"`.

1.  **Kit tray Gazebo frame name has changed.**

    The Gazebo frame of kit trays has changed from `agv1::kit_tray::kit_tray::tray` to `agv1::kit_tray_1::kit_tray_1::tray`. This frame is used for manually spawning models on trays during development, it is not used by participants programmatically.

1.  **Kit tray TF frames now unique.**

    The name of the TF frame of kit trays detected by logical cameras is now unique and of the form `kit_tray_{N}_frame` instead of `kit_tray_frame`.

1.  **Gripper fixed to work with lower realtime factors.**

    Some participants reported issues with the vacuum gripper not functioning on machines running ARIAC with low realtime factors. This has been resolved.

1.  **Conveyor belt 'power' setting.**

    The conveyor belt can be controlled with a `power` setting instead of velocity, e.g. `rosservice call /ariac/conveyor/control "state: {power: 50}"`. Control of the power of the belt is permitted for qualification task 2 but will not be permitted for the final competition.

1.  **Logical camera range reduced.**

    The logical camera has had its range changed from [0.55m, 5m] to [0.2, 2m].


## **Changes to ARIAC documentation**

### 2017-07-05
1. **Results of the finals announced.** [See here for the results.](https://www.osrfoundation.org/ariac-finals-results-announced/)
1. **Finals scenarios released** [into this repository](https://bitbucket.org/osrf/ariac/src/46d865c3ef88153de50640df410e57489bc655cd/osrf_gear/config/finals/?at=ariac_2017).

### 2017-06-01
1. **Time limit finalized.** 500 simulation seconds will be permitted for each trial. [See the Finals specifications page.](https://bitbucket.org/osrf/ariac/wiki/2017/finals_specs)

### 2017-06-01
1. **Scoring parameters finalized.** High-priority factor = 3, Cost factor multiplier = 4. [See the Scoring Metrics page.](https://bitbucket.org/osrf/ariac/wiki/2017/scoring)

### 2017-05-30
1. **Faulty part probability added.** [See the Finals specifications page.](https://bitbucket.org/osrf/ariac/wiki/2017/finals_specs)

### 2017-05-25
1. **Tips for improving real-time factor added.** [See "Improving real-time factor during development" in the competition configuration file documentation](https://bitbucket.org/osrf/ariac/wiki/2017/configuration_spec)

### 2017-05-25
1. **Finals details added.** [See this page for Finals specifications and submission procedure.](https://bitbucket.org/osrf/ariac/wiki/2017/finals)

### 2017-04-17
1. **Faulty part specification added.** [See 'Faulty parts' in the competition specifications](https://bitbucket.org/osrf/ariac/wiki/2017/competition_specifications#markdown-header-faulty-parts) and ['Faulty parts' in the interface tutorial](http://wiki.ros.org/ariac/Tutorials/GEARInterface#Faulty_parts).

### 2017-04-13
1. **Flipped part specification added.** [See 'Flipped parts' in the frame specifications](https://bitbucket.org/osrf/ariac/wiki/2017/frame_specifications#markdown-header-flipped-parts)

### 2017-04-10
1. **"All-parts" bonus is not given to kits with unwanted parts.** [See the scoring specifications.](https://bitbucket.org/osrf/ariac/wiki/2017/scoring)

### 2017-03-24
1. **Pose scoring tolerances documented.** [See the scoring specifications.](https://bitbucket.org/osrf/ariac/wiki/2017/scoring)

### 2017-03-06
1.  **Tray cheats added for use in development.** See http://wiki.ros.org/ariac/Tutorials/GEARInterface#Viewing_kit_contents and http://wiki.ros.org/ariac/Tutorials/GEARInterface#Submitting_trays_without_AGV_movement for examples.

1. **ARIAC update policy added.** [See this page for details.](https://bitbucket.org/osrf/ariac/wiki/2017/update_policy)

1.  **Technical support for MoveIt is not provided.** See http://wiki.ros.org/ariac/Tutorials/MoveItInterface#Troubleshooting for details.

### 2017-03-03
1.  **Binaries for ROS Kinetic added.** Previously binaries were only released for ROS Indigo users and ROS Kinetic users were required to build ARIAC from source.

### 2017-02-21
1.  **Gazebo minimum updated to 7.5.0.** Previously the minimum Gazebo version was listed as 7.0.0, which [is not sufficient](https://bitbucket.org/osrf/ariac/issues/38).

### 2017-02-08
1.  **Part frame specifications added.** The [part specifications page](https://bitbucket.org/osrf/ariac/wiki/2017/frame_specifications) has been added with information on the frames used in orders.

### 2017-01-27
1.  **Developer tips added.** The [developer tips page](https://bitbucket.org/osrf/ariac/wiki/2017/developer_tips) has been added with information for participants that may be useful during ARIAC development. Suggestions to this page are welcome by [opening an issue](https://bitbucket.org/osrf/ariac/issues).


## **Upcoming changes**

### 2017-05-10
1. **Improvements to laser profiler proposed.** [Update 2017-05-13: implemented]. The laser profiler sensor will have the following changes unless a team objects by May 12:

    - angular resolution increased from 100 points/scan to 400 points/scan
    - update rate increased from 20 Hz to 100 Hz.

    To test out the proposed changes, add the ARIAC pre-release repository with:

    ```
    sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-prerelease `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-prerelease.list'
    ```

    and then run `sudo apt-get update && sudo apt-get install ariac`. Your ARIAC version will be updated to 1.1.2 which will become the standard version if no objections are received.

   When you are finished testing we suggest you remove the `/etc/apt/sources.list.d/gazebo-prerelease.list` added in the above command.

### 2017-04-10
1. **Logical camera obstruction.**

    There is a known issue with the logical camera where models that are obstructed by other models in the view of the camera are still reported as visible. This will be resolved before the competition.
