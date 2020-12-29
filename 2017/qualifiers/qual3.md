# Introduction

This is the third qualification task for the Agile Robotics for Industrial Automation Competition (ARIAC). For full details about ARIAC and how to register for the qualification tasks, see [gazebosim.org/ariac](http://gazebosim.org/ariac).


_**Note to participants of the previous qualification tasks:** you must update your ARIAC software to the latest version (>1.1.0) to participate in this qualification task. Please read the [ARIAC news page](https://bitbucket.org/osrf/ariac/wiki/2017/updates) for details of changes to the ARIAC software that may require modifications to your software._

# Overview

ARIAC qualification task 3 has been designed to introduce you to additional challenges that will be present in the final competition so that you are better prepared as competitors.


Teams must complete at least one of the three qualifiers to participate in the final competition.
Participants are encouraged to complete as many qualifiers as possible, even though only one is required.
The second and third qualifiers will better prepare participants for the challenges presented in the competition. Participants who have not completed the previous qualification tasks are eligible and encouraged to participate in qualification task 3.

[The Competition Specifications](https://bitbucket.org/osrf/ariac/wiki/2017/competition_specifications) detail the full competition task scenarios.
As part of the third qualification task, you will have to complete two parts:

-   Part A: A simplified version of Scenario 3: In-process Kit Change.
    -   Parts will only be required to be retrieved from the stationary bins. The conveyor belt is not used.
-   Part B: A simplified version of Scenario 3: In-process Kit Change.
    -   Competitors are permitted to control the conveyor belt.

Both Part A and Part B have the following simplifications:

-   There is no time limit for the trials.
-   Only the completion score of the trials will be used to determine if a team qualifies for the final competition. Efficiency factors and the cost of sensors used will be calculated but not used to determine if teams qualify.

[**This page has more details on what to expect in the scenarios used in the third qualification task.**](https://bitbucket.org/osrf/ariac/wiki/2017/qualifiers/qual3_scenarios)

The task is to be completed on your machine, with resulting files submitted for evaluation.

To successfully qualify for the competition through this qualification task, competitors must have a combined completion score for the two trials of 10.

While full completion of the tasks in the third qualifier is recommended for teams to ensure that they are on-track to participate in the final competition, it is not required.
As such, **participants who have not completed the first or second qualification task are still encouraged to participate in this qualifier.**

# Important dates

**Qualification task 3 announced:** April 17 2017

**Submissions close:** May 15 2017

# Getting started

Before starting the qualification task, you should complete the following:

1.   Read through the [competition documentation](https://bitbucket.org/osrf/ariac/wiki/2017/documentation) to understand the high-level information about how the competition is run.
1.   Ensure that your machine satisfies the minimum [system requirements](https://bitbucket.org/osrf/ariac/wiki/2017/system_requirements).
1.   Complete the sequence of [tutorials](https://bitbucket.org/osrf/ariac/wiki/2017/tutorials) that have been developed to walk you through the process of competing in the competition.
1.   Consider completing the [previous qualification tasks](https://bitbucket.org/osrf/ariac/wiki/2017/qualifiers/qualifiers.md) that have been released to build up to completion of the final competition. Submissions will not be accepted but completion is encouraged.


# Files to submit

A submission for qualification task 3 requires six files.

1.  Your team information.
1.  Your environment configuration file specifying your sensor placement. **You must submit one environment configuration file that is to be used for both trials.**
1.  For each trial (Part A and Part B), a performance log file that contains information about the task completion.
1.  For each trial (Part A and Part B), a simulation state log file that contains information about the state of Gazebo during the trial.

See [the logging page](https://bitbucket.org/osrf/ariac/wiki/2017/qualifiers/logging) for details on the log files to be submitted.

# Uploading your submission files

You will need to submit a zip file with the following file structure:


```
- /ariac_qual3
  - my_team.txt
  - my_team_config.yaml
    - /qual3a
      - performance.log
      - /gazebo
        - state.log
    - /qual3b
      - performance.log
      - /gazebo
        - state.log
```

The `my_team.txt` file contains information about your team: the team name and members.

# Qualification task procedure

The qualification task is to be run on your own machine, with the relevant files submitted for evaluation.
This section details how you are to submit these files.

**Note**: this qualification task procedure is different to that of the final competition, where your code will be submitted so that it can be run against **unseen** competition configuration files.

**Note**: the only cheat permitted for this qualification task is the control of the conveyor belt. Submissions must have been run with ARIAC run in _competition mode_, **not** with [cheats](https://bitbucket.org/osrf/ariac/wiki/2017/competition_interface_documentation#markdown-header-cheats) enabled. The conveyor belt control will still work.

1.  Develop your package to complete the task following [the Hello World tutorial](http://wiki.ros.org/ariac/Tutorials/HelloWorld).

1.  Run part A of the qualification task, being sure to specify your environment configuration file:

    ```
    rosrun osrf_gear gear.py -f `catkin_find --share osrf_gear`/config/qual3a.yaml <path_to_your_config_file>.yaml
    ```

1.  Run your node(s) to interface with the ARIAC simulation.

1.  Create a directory for the submission.

    ```
    $ mkdir -p ~/ariac_qual3
    ```

1.  Copy the log files for Part A:

    ```
    $ cp --recursive --dereference ~/.ariac/log ~/ariac_qual3/qual3a
    ```

1.  Repeat steps 2-3 using Part B of the qualification task:

    ```
    rosrun osrf_gear gear.py -f `catkin_find --share osrf_gear`/config/qual3b.yaml <path_to_your_config_file>.yaml
    ```

1.   Copy the log files for Part B:

    ```
$ cp --recursive --dereference ~/.ariac/log ~/ariac_qual3/qual3b
    ```

1.  Copy your team's configuration file:

    ```
$ cp <path_to_your_config_file>.yaml ~/ariac_qual3
    ```

1.  Copy your team description file:

    ```
$ cp <path_to_your_team_description>.txt ~/ariac_qual3
    ```

1.  Create a tarball of your submission files:

    ```
$ tar -zcvf <team_name>_qual3.tar.gz ~/ariac_qual3
    ```

Submit the resulting `<team_name>_qual3.tar.gz` file using the submission link that you received when you registered for the qualification task.

You are also encouraged to submit a tarball of your source code. While this is not mandatory for the  qualifiers, submitting your source code will be necessary when competing in the competition in June 2017. Submitting your source code helps us to ensure that we support the relevant dependencies that are used by teams. All code will be kept confidential.


# Characteristics of a valid submission

Valid submissions for the third qualification task have the following characteristics. Please ensure that your submission meets these standards in order for it to be reviewed.

- The latest version of the ARIAC software has been used. For teams building the ARIAC software from source, the latest commit on the `master` branch has been used.
- **One** sensor configuration file is used for all submitted trials.
- The team's code interfaces with the ARIAC simulation using only [the permitted ROS interfaces](https://bitbucket.org/osrf/ariac/wiki/2017/competition_interface_documentation). Cheats are not permitted: the ARIAC software must not have been run with `--development-mode` enabled.
- The ARIAC software for each trial submitted reaches the `done` state (according to `/ariac/competition_state`). This is accomplished by either submitting all kits in the requested orders, or manually calling the `/ariac/end_competition` service. This is required for scores to be recorded correctly.
- The Qualification Task Procedure specified above has been followed. This ensures that the log files are submitted correctly.

# Where to go for help
We strive to provide responsive and high-quality support for our software.
Please use [the GEAR/ARIAC issue tracker](https://bitbucket.org/osrf/ariac/issues?status=new&status=open) for submitting and following bugs, feature requests and enhancements.

If you have any questions about competition specifics that you would like to ask in private, please contact ariac@nist.gov.

You can use [the GEAR/ARIAC support forum](https://discourse.ros.org/c/ariac-users) for public discussions about the competition in which other competition participants may participate.
