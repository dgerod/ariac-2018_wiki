# Introduction

This is the first qualification task for the Agile Robotics for Industrial Automation Competition (ARIAC). For full details about ARIAC and how to register for the first qualification task, see [gazebosim.org/ariac](http://gazebosim.org/ariac).

# Overview

ARIAC qualification task 1 has been designed to get you familiar with the ARIAC system so that you are better prepared for the full competition.

[The Competition Specifications](https://bitbucket.org/osrf/ariac/wiki/2017/competition_specifications) detail the full competition task scenarios.
As part of the first qualification task, you will have to complete two parts:

-   Part A: A simplified version of Scenario 1: Baseline Kit Building.
-   Part B: A simplified version of Scenario 2: Dropped Part.

The scenarios are simplified in the following way:

-   Parts will only be required to be retrieved from the stationary bins. The conveyor belt is not used.
-   There is no time limit for the trials.
-   The completion of each trial will be pass/fail: you will pass if you submit the appropriate order with the correct parts, no matter their poses. Your score will not be evaluated.

The task is to be completed on your machine, with resulting files submitted for evaluation.

# Important dates

**Qualification task 1 announced:** January 27 2017

**Submissions close:** February 24 2017

# Getting started
Before starting the qualification task, you should complete the following:

1.   Read through the [competition documentation](https://bitbucket.org/osrf/ariac/wiki/2017/documentation) to understand the high-level information about how the competition is run.
1.   Ensure that your machine satisfies the minimum [system requirements](https://bitbucket.org/osrf/ariac/wiki/2017/system_requirements).
1.   Complete the sequence of [tutorials](https://bitbucket.org/osrf/ariac/wiki/2017/tutorials) that have been developed to walk you through the process of competing in the competition.

# Files to submit

A submission for qualification task 1 requires five files.

1.  Your environment configuration file specifying your sensor placement.
1.  For each trial (Part A and Part B), a performance log file that contains information about the task completion.
1.  For each trial (Part A and Part B), a simulation state log file that contains information about the state of Gazebo during the trial.

### Log files
Log files for each run are written to the `~/.ariac/log` directory.

**Log files are over-written with every run or playback of the ARIAC software, so make a backup of your submission files before running more trials.** As the performance log is a symbolic link to another file, be sure to use the `cp --dereference` option when copying the `~/.ariac/log` directory.

#### 1. Task performance log file

The task performance log file is written to `~/.ariac/log/performance.log`.
This file will be reviewed to evaluate your performance in the task.

*Note: if you are using a gazebo port other than the default (11345), your task performance log file will be at `~/.gazebo/server-<port number>/default.log`.*

#### 2. Simulation state log file

The simulation state log file is written to `~/.ariac/log/gazebo/state.log`.
This log stores all of the simulation data during the trial and may be used to confirm your task performance log file.

It's highly recommended that you review your log files before submission, using:

```
roslaunch osrf_gear gear_playback.launch
# Or, if you want to specify a specific log file:
roslaunch osrf_gear gear_playback.launch state_log_path:=`pwd`/qual_1.log
```

Don't worry if you see the following warning, it's safe to ignore it:
```
[Wrn] [msgs.cc:1793] Conversion of sensor type[logical_camera] not suppported.
```

If you see the following error:
```
[Err] [Master.cc:96] EXCEPTION: Unable to start server[bind: Address already in use]. There is probably another Gazebo process running.
```

then you may find `pkill -f gzserver` useful for killing gazebo servers that have not closed properly.

# Uploading your submission files

You will need to submit a zip file with the following file structure:


```
- /ariac_qual1
  - my_team.txt
  - my_team_config.yaml
    - /qual1a
      - performance.log
      - /gazebo
        - state.log
    - /qual1b
      - performance.log
      - /gazebo
        - state.log
```

The `my_team.txt` file contains information about your team: the team name and members.

# Qualification task procedure

The qualification task is to be run on your own machine, with the relevant files submitted for evaluation.
This section details how you are to submit these files.

**Note**: this qualification task procedure is different to that of the final competition, where your code will be submitted so that it can be run against **unseen** competition configuration files.

1.  Develop your package to complete the task following [the Hello World tutorial](http://wiki.ros.org/ariac/Tutorials/HelloWorld).

1.  Run part A of the qualification task, being sure to specify your environment configuration file:

    ```
    rosrun osrf_gear gear.py -f `catkin_find --share osrf_gear`/config/qual1a.yaml <path_to_your_config_file>.yaml
    ```

1.  Run your node(s) to interface with the ARIAC simulation.

1.  Create a directory for the submission.

    ```
    $ mkdir -p ~/ariac_qual1
    ```

1.  Copy the log files for Part A:

    ```
    $ cp --recursive --dereference ~/.ariac/log ~/ariac_qual1/qual1a
    ```

1.  Repeat steps 2-3 using Part B of the qualification task:

    ```
    rosrun osrf_gear gear.py -f `catkin_find --share osrf_gear`/config/qual1b.yaml <path_to_your_config_file>.yaml
    ```

1.   Copy the log files for Part B:

    ```
$ cp --recursive --dereference ~/.ariac/log ~/ariac_qual1/qual1b
    ```

1.  Copy your team's configuration file:

    ```
$ cp <path_to_your_config_file>.yaml ~/ariac_qual1
    ```

1.  Copy your team description file:

    ```
$ cp <path_to_your_team_description>.txt ~/ariac_qual1
    ```

1.  Create a tarball of your submission files:

    ```
$ tar -zcvf <team_name>.tar.gz ~/ariac_qual1
    ```

Submit the resulting `<team_name>.tar.gz` file using the submission link that you received when you registered for the qualification task.

You are also encouraged to submit a tarball of your source code. While this is not mandatory for the first qualifier, submitting your source code will be necessary when competing in the competition in June 2017. Submitting your source code helps us to ensure that we support the relevant dependencies that are used by teams. All code will be kept confidential.

# Where to go for help
We strive to provide responsive and high-quality support for our software.
Please use [the GEAR/ARIAC issue tracker](https://bitbucket.org/osrf/ariac/issues?status=new&status=open) for submitting and following bugs, feature requests and enhancements.

If you have any questions about competition specifics that you would like to ask in private, please contact ariac@nist.gov.

You can use [the GEAR/ARIAC support forum](https://discourse.ros.org/c/ariac-users) for public discussions about the competition in which other competition participants may participate.