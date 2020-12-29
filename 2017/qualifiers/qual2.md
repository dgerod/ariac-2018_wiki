# Introduction

This is the second qualification task for the Agile Robotics for Industrial Automation Competition (ARIAC). For full details about ARIAC and how to register for the qualification tasks, see [gazebosim.org/ariac](http://gazebosim.org/ariac).

# Overview

ARIAC qualification task 2 has been designed to introduce you to additional challenges that will be present in the final competition so that you are better prepared as competitors.


Teams must complete at least one of the three qualifiers to participate in the final competition.
Participants are encouraged to complete as many qualifiers as possible, even though only one is required.
The second and third qualifiers will better prepare participants for the challenges presented in the competition. Participants who have not completed qualification task 1 are eligible and encouraged to participate in qualification task 2.

[The Competition Specifications](https://bitbucket.org/osrf/ariac/wiki/2017/competition_specifications) detail the full competition task scenarios.
As part of the second qualification task, you will have to complete two parts:

-   Part A: A simplified version of Scenario 2: Dropped Part.
    -   Parts will only be required to be retrieved from the stationary bins. The conveyor belt is not used.
-   Part B: A simplified version of Scenario 1: Baseline Kit Building.
    -   Competitors are permitted to control the conveyor belt.

Both Part A and Part B have the following simplifications:

-   There is no time limit for the trials.
-   Only the completion score of the trials will be evaluated. Efficiency factors and the cost of sensors used will not be evaluated.

[This page](https://bitbucket.org/osrf/ariac/wiki/2017/qualifiers/qual2_scenarios) has more details on the scenarios used in the task.

The task is to be completed on your machine, with resulting files submitted for evaluation.

To successfully qualify for the competition through this qualification task, competitors must have a combined completion score for the two trials of 10.

While full completion of the tasks in the second qualifier is recommended for teams to ensure that they are on-track to participate in the final competition, it is not required.
As such, **participants who have not completed the first qualification task are still encouraged to participate in this qualifier.**

# Important dates

**Qualification task 2 announced:** March 6 2017

**Submissions close:** April 3 2017

# Getting started

Before starting the qualification task, you should complete the following:

1.   Read through the [competition documentation](https://bitbucket.org/osrf/ariac/wiki/2017/documentation) to understand the high-level information about how the competition is run.
1.   Ensure that your machine satisfies the minimum [system requirements](https://bitbucket.org/osrf/ariac/wiki/2017/system_requirements).
1.   Complete the sequence of [tutorials](https://bitbucket.org/osrf/ariac/wiki/2017/tutorials) that have been developed to walk you through the process of competing in the competition.


**Note to participants of the first qualification task:** you must update your ARIAC software to the latest version (>1.0.0) to participate in this qualification task. Please read the [ARIAC news page](https://bitbucket.org/osrf/ariac/wiki/2017/updates) for details of changes to the ARIAC software that may require modifications to your software.

# Files to submit

A submission for qualification task 2 requires six files.

1.  Your team information.
1.  Your environment configuration file specifying your sensor placement. **You must submit one environment configuration file that is to be used for both trials.**
1.  For each trial (Part A and Part B), a performance log file that contains information about the task completion.
1.  For each trial (Part A and Part B), a simulation state log file that contains information about the state of Gazebo during the trial.

See [the logging page](https://bitbucket.org/osrf/ariac/wiki/2017/qualifiers/logging) for details on the log files to be submitted.

# Uploading your submission files

You will need to submit a zip file with the following file structure:


```
- /ariac_qual2
  - my_team.txt
  - my_team_config.yaml
    - /qual2a
      - performance.log
      - /gazebo
        - state.log
    - /qual2b
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
    rosrun osrf_gear gear.py -f `catkin_find --share osrf_gear`/config/qual2a.yaml <path_to_your_config_file>.yaml
    ```

1.  Run your node(s) to interface with the ARIAC simulation.

1.  Create a directory for the submission.

    ```
    $ mkdir -p ~/ariac_qual2
    ```

1.  Copy the log files for Part A:

    ```
    $ cp --recursive --dereference ~/.ariac/log ~/ariac_qual2/qual2a
    ```

1.  Repeat steps 2-3 using Part B of the qualification task:

    ```
    rosrun osrf_gear gear.py -f `catkin_find --share osrf_gear`/config/qual2b.yaml <path_to_your_config_file>.yaml
    ```

1.   Copy the log files for Part B:

    ```
$ cp --recursive --dereference ~/.ariac/log ~/ariac_qual2/qual2b
    ```

1.  Copy your team's configuration file:

    ```
$ cp <path_to_your_config_file>.yaml ~/ariac_qual2
    ```

1.  Copy your team description file:

    ```
$ cp <path_to_your_team_description>.txt ~/ariac_qual2
    ```

1.  Create a tarball of your submission files:

    ```
$ tar -zcvf <team_name>_qual2.tar.gz ~/ariac_qual2
    ```

Submit the resulting `<team_name>_qual2.tar.gz` file using the submission link that you received when you registered for the qualification task.

You are also encouraged to submit a tarball of your source code. While this is not mandatory for the  qualifiers, submitting your source code will be necessary when competing in the competition in June 2017. Submitting your source code helps us to ensure that we support the relevant dependencies that are used by teams. All code will be kept confidential.

# Where to go for help
We strive to provide responsive and high-quality support for our software.
Please use [the GEAR/ARIAC issue tracker](https://bitbucket.org/osrf/ariac/issues?status=new&status=open) for submitting and following bugs, feature requests and enhancements.

If you have any questions about competition specifics that you would like to ask in private, please contact ariac@nist.gov.

You can use [the GEAR/ARIAC support forum](https://discourse.ros.org/c/ariac-users) for public discussions about the competition in which other competition participants may participate.
