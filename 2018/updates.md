# ARIAC competition software updates

_These updates are posted to [this forum thread](https://discourse.ros.org/t/ariac-code-release-updates/4009), which participants can subscribe to for notifications._

## **Changes to ARIAC software**
_To determine the version of the ARIAC software that you're running, check the `~/.ariac/log/performance.log` file, which will contain e.g. "ARIAC VERSION: 2.0.2"._
_To update your ARIAC software, run `sudo apt-get update && sudo apt-get install ariac2`._

_With each ARIAC software release, a new version of the [automated evaluation setup](https://bitbucket.org/osrf/ariac/wiki/2018/automated_evaluation) will be released that uses the latest ARIAC version. See [these instructions](https://github.com/osrf/ariac-docker/blob/master/README.md#keeping-the-competition-setup-software-up-to-date) for how to update._

### Version 2.1.8 (21 May 2018)
1. **Finals scenarios released.** The config files used for the Finals of the competition are in the `config/finals` directory. [This page gives an overview of each trial](https://bitbucket.org/osrf/ariac/wiki/2018/finals_scenarios).
1. **State logs recorded at lower frequency.** (This change was included in the version of ARIAC used for evaluating the Finals).
1. **Fix state log playback of shipping boxes.** Closing/collection of shipping boxes during log playback now works correctly during state log playback.

### Version 2.1.7 (19 April 2018, used for evaluating the Finals)
1. **qual2b.yaml released.** The config file that was used for evaluating Part B of the second qualifier is in `config/quals/qual2b.yaml`.
1. **Conveyor belt simulation model update.** The simulation model of the conveyor belt has been updated to  make [this issue](https://bitbucket.org/osrf/ariac/issues/115), where boxes fall into the conveyor belt, less likely to occur. There should be no other observable impact to users.

### Version 2.1.6 (12 April 2018, used for evaluation of Qualification Task 2)
1. **Rollback to 2.1.5~pre1.** Two "pre-release" versions of 2.1.5 were released to users for testing prior to yesterday's ariac2.1.5 release to improve IIWA14 controller performance: 2.1.5~pre1 and 2.1.5~pre2. The version released yesterday was 2.1.5~pre2; ariac2.1.6 rolls back to 2.1.5~pre1 based on feedback from participants that it provides better arm performance.


### Version 2.1.5 (11 April 2018)
1. **IIWA14 model/controller modifications.** The arm simulation model/controller has been updated to avoid an issue with joint 7 getting stuck/causing instability, and to relax tolerances on the trajectory controller ([see this issue for details](https://bitbucket.org/osrf/ariac/issues/126)). Participants should update their version to test the changes before submitting their qual2 submission, as the most recently released ARIAC version will be used for the qualifier evaluation.

### Version 2.1.4 (4 April 2018)
1. **Fixed bug with box being spawned on competition start.** [This issue](https://bitbucket.org/osrf/ariac/issues/116), which would occur occasionally for some participants, has been resolved.
1. **Updated shipping box collisions.** The external walls of shipping boxes have been widened to make [this issue](https://bitbucket.org/osrf/ariac/issues/115), where boxes would fall into the conveyor belt, less likely to occur. The internal dimensions of the boxes are unchanged.

### Version 2.1.3 (2 April 2018, Qualification Task 2 release)
1. **Qualification task 2 Part A trial config file released.** See [the second qualifier page](https://bitbucket.org/osrf/ariac/wiki/2018/qualifiers/qual2) for details.

### Version 2.1.2 (30 March 2018)
1. **Example of the sensor blackout challenge released.** Read/use `sample_sensor_blackout.yaml` for practice. Note that re-connecting to some sensors during development will cause them to resume publishing data, but this functionality is blocked in the automated evaluation setup.
1. **ROS interface to the `congestion_sensor` removed.** This is the break beam positioned at the end of the conveyor belt by default.
1. **Conveyor control blocked before competition start.** Service calls to set the conveyor belt power before the competition has been started will fail.

### Version 2.1.1 (27 March 2018)
1. **Example of the dropped product challenge released.** Read/use `sample_dropped_products.yaml` for practice.
1. **Example of the order update challenge released.** Read/use `sample_order_update.yaml` for practice.
1. **qual1b.yaml released.** The config file that was used for evaluating Part B of the first qualifier is in `config/quals/qual1b.yaml`.
1. **Information about product types not from sensors removed.**
    1. The `/ariac/material_locations` service and the `/ariac/current_score` topic have been re-classified as cheats.
    1. The quality control sensors now publish anonymized model names instead of the types of the faulty products that are detected. As a side effect, the model numbering scheme has been updated; any randomized faulty product IDs in custom-defined trial configs will need to be updated.
1. **Devel space support.** Use of the devel space is now supported for users building from source (contributed by @IanTheEngineer).

### Version 2.1.0 (21 March 2018)
1. **UR10 replaced by the Kuka IIWA14.** The IIWA14 will be used in all future trials; the UR10 will no longer be used. The IIWA14 presents the same ROS interface but **participants will need to update their system to adapt to the new arm**. This was announced as an upcoming change on 17 February 2018.
1. **Updated environment.** The workcell environment, particularly the shipping container, shelving and the conveyor belt, has been updated to accommodate the working area of the IIWA14. **Teams will need to re-position their sensors.** The dimensions of the shipping boxes, storage bins, and products have not been modified.

### Version 2.0.6 (14 March 2018, used for evaluation of Qualification Task 1)
1. **Option to use joint-limited UR10.** By default the UR10 has joint limits of `[-2*PI, 2*PI]`; there is now an option to use joint limits of `[-PI, PI]`, which provides better controller performance [in some situations](https://bitbucket.org/osrf/ariac/issues/106/wrist-1-joint-has-issues-wrapping-get). It can be enabled by adding `joint_limited_ur10: true` to your team's config file [similarly to this](https://bitbucket.org/osrf/ariac/src/bf4daee64d7528572fb0644d7686fd9d856587c2/osrf_gear/config/sample_user_config.yaml?fileviewer=file-view-default#sample_user_config.yaml-1). Participants that do not wish to enable this option do not need to make any changes to their system. The use of this option is permitted in submissions for the first qualifier. If you're using MoveIt!, you might need to add `limited:=true` to your `ur10_moveit_planning_execution` launch invocation.
1. **New Gazebo release.** The `ariac2-server` Docker image used in [automated evaluation setup](https://bitbucket.org/osrf/ariac/wiki/2018/automated_evaluation) has been updated to use gazebo8.4 now that the logging issues have been resolved.

### Version 2.0.5 (8 March 2018)
1. **Product IDs randomized.** For all future trial config files released (including qual1b), products in the storage bins will no longer have sequential IDs.
1. **Updated environment collisions.** Fixed misalignment of the vertical bars in the support frame around the storage bins.
1. **`pulley_part` model updated.** It is now asymmetric on top and bottom. Pulleys (and all other products) will always start un-flipped in the storage bins.


### Version 2.0.4 (5 March 2018, Qualification Task 1 release)
1. **Qualification task 1 Part A trial config file released.** See [the first qualifier page](https://bitbucket.org/osrf/ariac/wiki/2018/qualifiers/qual1) for details.
1. **More environment collisions.** The arm can no longer pass through the support frame around the storage bins. This was advised as an upcoming change on 17 February.
1. **Reduced logical camera FOV.** In response to the additional workcell collisions, the logical camera range has been reduced.
1. **Segfault on competition start fixed.** This would happen if the `/ariac/start_competition` service was called before the simulation had finished loading.

### Version 2.0.3 (28 February 2018)
1. **Additional sample trial config files released.** See [the trial configuration tutorial](https://bitbucket.org/osrf/ariac/wiki/2018/configuration_spec) for how to launch the trials. Summary of new trial config files (more details in the files themselves):
    1. `sample_interruption1.yaml`: high priority order interruption at a "convenient" time.
    1. `sample_interruption2.yaml`: high priority order interruption at an "inconvenient" time.
    1. `sample_flipped.yaml`: order requiring products to be flipped ([see 'Flipped products' in the frame specifications](https://bitbucket.org/osrf/ariac/wiki/2018/frame_specifications#markdown-header-flipped-products)).
    1. `sample_not_enough_products.yaml`: order requiring more products than available for use.

### Version 2.0.2 (17 February 2018)
1. **First version of software released.** Teams should read through the documentation and follow the tutorials listed at on [the ARIAC 2018 wiki](https://bitbucket.org/osrf/ariac/wiki/2018/Home). Key changes from the 2017 software:
    1. Order fulfilment in a shipping container with handoff to a drone for delivery.
    1. Orders filled on shipping boxes that move along the belt instead of stationary kits over AGVs.
    1. Control of the conveyor belt is permitted.
    1. Depth camera added as a sensor option for teams using perception for object detection.
    1. Lower scan rate for the laser profiler; larger scan angle.


## **Changes to ARIAC documentation**

### 19 April 2018
1. **Finals schedule released.** The [Finals wiki page](https://bitbucket.org/osrf/ariac/wiki/2018/finals) has been released, including details on what to expect in the Finals, dry-run testing on the competition machines, and the schedule of the process.
1. **Automated evaluation results structure outlined.** Structure of the `logs` directory output by the automated evaluation setup is now described [in the readme](https://github.com/osrf/ariac-docker/blob/master/README.md#reviewing-the-trial-performance).

### 12 April 2018
1. **Trial time limit clarification.** As mentioned in [the details of qual2 scenarios](https://bitbucket.org/osrf/ariac/wiki/2018/qualifiers/qual2_scenarios), 500 sim seconds will be used for qual2b. The [competition specifications](https://bitbucket.org/osrf/ariac/wiki/2018/competition_specifications) now clarify that this information is not broadcast by the ARIAC server. For the Finals, as with the Qualifiers, the time limit will be set as a fixed value for all trials, which teams will know in advance. There are no time limits for individual orders.

### 11 April 2018
1. **Product scoring limitation.** The [scoring metrics](https://bitbucket.org/osrf/ariac/wiki/2018/scoring) page now clarifies that products must be placed onto the base of the shipping box to be counted for scoring, not on top of other products.


### 4 April 2018
1. **Gazebo version 8.4 required.** The [system requirements](https://bitbucket.org/osrf/ariac/wiki/2018/system_requirements) have been updated to highlight that Gazebo 8.4 is required to avoid issues with state logging recording/playback.
1. **Agility challenge page added.** [This page](https://bitbucket.org/osrf/ariac/wiki/2018/agility_challenges) has been added, which summarizes the released agility challenges including additional details on the "sensor blackout" challenge.

### 30 March 2018
1. **Sensor placement rules clarified.** The [competition specifications](https://bitbucket.org/osrf/ariac/wiki/2018/competition_specifications) now detail that sensors can be placed in any free space in the workcell, they do _not_ need to be mounted such that they are touching the conveyor belt/support frame of the storage bin.
Sensors must be used in a realistic manner and must not exploit any simulation technicalities such as the logical camera seeing through obstructions.

### 27 March 2018
1. **Sample trial configs highlighted.** The [configuration file tutorial](https://bitbucket.org/osrf/ariac/wiki/2018/configuration_spec) has been updated to highlight that sample config files are available for practicing with.

### 21 March 2018
1. **Tutorials updated for IIWA14.** Tutorials involving control of the robot arm have been updated for the switch to the IIWA14.

### 18 March 2018
1. **Re-run policy clarified.** Re-runs for [the first qualifier](https://bitbucket.org/osrf/ariac/wiki/2018/qualifiers/qual1) will be permitted only in the event of simulation bugs such as reported issues [#115](https://bitbucket.org/osrf/ariac/issues/115) and [#116](https://bitbucket.org/osrf/ariac/issues/116), at the discretion of the competition controllers. Bugs in competitors' code does not warrant a re-run.

1. **Enabling state logging in `qual1a.yaml`.** [The qual1 scenario description page](https://bitbucket.org/osrf/ariac/wiki/2018/qualifiers/qual1_scenarios) has been updated to clarify that simulation state logging will be enabled in the first qualifier trials via the `gazebo_state_logging: true` setting in the the trial config file. If the config file that you are testing with in the automated evaluation setup does not have logging explicitly enabled [like this](https://bitbucket.org/osrf/ariac/src/4949e714932794b40513f6660d1af119148e2d67/osrf_gear/config/quals/qual1a.yaml?fileviewer=file-view-default#qual1a.yaml-20), please add that line to the config file to enable logging.

### 14 March 2018
1. **Submission process for the first qualifier updated.** Teams must have had a secure workspace created by competition controllers before they can upload their submissions for [the first qualifier](https://bitbucket.org/osrf/ariac/wiki/2018/qualifiers/qual1).
1. **Scoring metrics released.** See [this page](https://bitbucket.org/osrf/ariac/wiki/2018/scoring). Note that these may change between rounds of the competition.
1. **Qualifying guidelines for the first qualifier updated.** Clarified that only automated evaluation metrics will be used for [the first qualifier](https://bitbucket.org/osrf/ariac/wiki/2018/qualifiers/qual1) and that any participants found violating submission guidelines (e.g. by starting the conveyor belt before starting the competition) will not be permitted to qualify for the Finals.
1. **ROS API clarifications.** `/ariac/end_competition`, `/ariac/competition_state`, `/ariac/drone/state`, `/ariac/current_score`, `/ariac/drone` topics/services documentation added/updated in [the competition interface documentation](https://bitbucket.org/osrf/ariac/wiki/2018/competition_interface_documentation).
    1. Clarified that requesting that the drone deliver any unknown shipment type will cause the drone to remove the box without scoring it.


### 7 March 2018
1. **Qualification task 1 Part B limitations clarified.** In particular, info on the storage bins, quality control sensors, potential products, and potential order count. See [this page](https://bitbucket.org/osrf/ariac/wiki/2018/qualifiers/qual1_scenarios) for the added details.
1. **Static sensors only.** [The environment configuration tutorial](https://bitbucket.org/osrf/ariac/wiki/2018/configuration_spec)/competition specifications have been updated to clarify that sensors can only be placed in static locations around the environment, they cannot be attached to the arm.



### 5 March 2018
1. **First qualifier announced.** See [this page](https://bitbucket.org/osrf/ariac/wiki/2018/qualifiers/qual1) for details.
1. **Logging/log files documented.** See [the logging page](https://bitbucket.org/osrf/ariac/wiki/2018/logging) for how to enable/playback simulation state logging for debug purposes.
1. **Update policy extended.** [The update policy](https://bitbucket.org/osrf/ariac/wiki/2018/update_policy) now covers rules/scoring metrics in addition to software changes.

### 17 Februrary 2018
1. **Initial documentation release.**


## **Upcoming changes**


### Proposed 10 April 2018

1. _IIWA controller updates. Update 11 April: released in ariac2.1.5._

    The controller has been updated to avoid an issue with joint 7 getting stuck, and to relax tolerances on the trajectory controller ([see this issue for details](https://bitbucket.org/osrf/ariac/issues/126)).

    To test out the proposed changes, add the ARIAC pre-release repository with:

    ```
    sudo sh -c 'echo "deb http://packages.osrfoundation.org/gazebo/ubuntu-prerelease `lsb_release -cs` main" > /etc/apt/sources.list.d/gazebo-prerelease.list'
    ```

    and then run `sudo apt-get update && sudo apt-get install ariac2`. Your ARIAC version will be updated to 2.1.5, which will become the standard version if no regressions are reported. Please report regressions on the issue linked above.

    When you are finished testing we suggest you remove the `/etc/apt/sources.list.d/gazebo-prerelease.list` added in the above command.

### Announced 14 March 2018

1. _`/ariac/current_score` topic classified as a 'cheat'. Update 27 March: released in ariac2.1.1._

    After the first qualification task closes the `/ariac/current_score` topic will become classified as a cheat.

### Announced 7 March 2018
1. _Docker images using gazebo8. Update 14 March: the `ariac2-server` Docker image for ariac.2.0.6 is using gazebo8.4._

    Docker images used for the [automated evaluation setup](https://bitbucket.org/osrf/ariac/wiki/2018/automated_evaluation) are currently using gazebo7.7 to avoid state log recording issues, but will be swapped to the next gazebo version when it is released (within the next week).

1. _State logging playback freeze fix. Update 14 March: released in gazebo8.4_

    A fix for the simulation state log playback freezing with gazebo8.3 will be resolved in the next Gazebo release. This impacts teams looking to playback state logs from the automated evaluation setup. See [these instructions](https://bitbucket.org/osrf/ariac/issues/95/state-log-from-automated-evaluation-wont#comment-43778689) for how to install gazebo8.2 as a temporary fix.

1. _`/ariac/material_locations` service classified as a 'cheat'. Update 27 March: released in ariac2.1.1._

    After the first qualification task closes the `/ariac/material_locations` service will become classified as a cheat. Teams will need to use sensors to infer the products available in storage bins.

1. _Model naming system change. Update March 8: released in ariac2.0.5._

    In ariac2.0.4, models in the environment of a particular type have sequential IDs. The naming system will be modified so that model IDs are randomized. As a result, logical cameras/quality control sensors will not publish TF frames, which include model IDs, correlated to the number of models in the environment.

1. _Conveyor controllable only after competition has started. Update 30 March: released in ariac2.1.2._

    In ariac2.0.4, the conveyor can be controlled before the competition has been started. This functionality will be removed and must not be exploited by teams.

### Announced 5 March 2018
1. _State logging fixes. Update 14 March: released in gazebo8.4_

    Fixes for the simulation state logging (low RTF during recording, no arm inserted during playback) will be resolved in the next Gazebo release.

1. _Scoring of ambiguous yaw. Update 8 March: released in ariac2.0.5._

    The `pulley_part` product's yaw is not distinguishable with perception sensors, but its yaw is evaluated by the scoring algorithm. This will be corrected for, either by making the yaw perceivable or by having the scoring algorithm ignore the yaw.


### Announced 17 February 2018
1. _Change of robot arm. Update 5 March: released in ariac2.1.0._

    ariac2.0.2 has been released with support for the UR10 arm. A different robot arm will be used in future versions: teams should use an abstract interface to work with the arm in preparation for changing to support the new arm. Support for the new arm will require modifications to the relative distances in the workcell environment: teams can use the TF frames published by the simulation to infer the location of components in the environment, e.g. the conveyor belt.

1. _Additional workcell collisions. Update 5 March: released in ariac2.0.4._

    The arm is currently able to pass through the support frame around the storage bins. Additional collisions in the simulation will be added to prevent this.

1. _Additional task challenges. Update 30 March: product drops and order updates have been introduced in ariac2.1.1 and sensor blackout has been introduced in ariac2.1.2._

    Additional task challenges such as order interruption and product drops will be added in future releases.