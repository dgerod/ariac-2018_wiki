# Finals

***[Update June 2017] Finals have wrapped up and the scenarios have been released into this repository. [See here for the outcome!](https://www.osrfoundation.org/ariac-finals-results-announced/)
***

During ARIAC qualifiers, teams were provided various scenarios and challenged to design a system that could adapt to those scenarios.
For the Finals, each team will submit their system so that it can be run against previously-unseen scenarios.
Teams participating in the qualifiers have already been exposed to all of the challenges that will be present in the Finals scenarios, but there is now the added challenge of designing a single system that is agile enough to react to each of the scenarios without knowing which agility challenges will occur and when.

## What to expect

[The Finals specifications page](https://bitbucket.org/osrf/ariac/wiki/2017/finals_specs) has details on how the competition will be evaluated and what can be expected in the unseen competition scenarios.

## Preparing your system

During qualifiers, teams have been exposed to 6 different scenarios generated by distinct competition configuration files.
[The competition configuration file specifications page](https://bitbucket.org/osrf/ariac/wiki/2017/configuration_spec) has details on how teams can create custom trial configuration files to test their system against additional scenarios.

## Submission process

Each team's system will be evaluated automatically against 15 scenarios.
To allow the ARIAC competition controllers to automatically run each team's system, teams are required to submit the following files:

- `team_config.yaml`: Their team's sensor configuration file.
- `build_team_system.bash`: A bash script that, when invoked from the command-line on a clean Ubuntu system, will install the necessary dependencies and build the team's code.
- `run_team_system.bash`: A bash script that, when invoked from the command-line on a system that has had `build_team_system.bash` run, will start the team's system and begin interacting with the ARIAC competition trial.
- `ros_distro.txt` (optional): A text file that contains only the word `indigo` or `kinetic`, representing the ROS distribution that the system uses. If not provided, `indigo` will be assumed.

The `build_team_system.bash` script will be run once to setup the team's system, and the `run_team_system.bash` script will be run 15 times: once for each of the scenarios.
The score for each of the 15 trial runs will be recorded automatically and then reviewed manually.

Submissions will be made through secure workspaces directly with competition controllers. If your team's code is not open source, you can include access keys in your setup script: they will not be made public.

## Preparing for submission

Teams should test their submission using the instructions provided at https://github.com/osrf/ariac-docker.
It is imperative that teams use the outlined process for testing their system, as it exactly replicates the process that will be used for the Finals.

## Pre-Finals dry-run testing of submissions

Teams will be able to submit their system for testing on the machine used to run the competition for a limited amount of time before the Finals.
The ARIAC competition team will work with teams to resolve any problems related to building/running of their system on that machine.
Teams must follow the testing procedure described above to reduce the risk of their system not being portable.

### Submission instructions
Once you have tested your system with the mock competition setup, zip the submission files in your team's directory with:

```
cd ~/ariac_ws/ariac-docker/team_configs
tar -zcvf <team_name>_prefinals.tar.gz <team_name>
```

Submit that tarball to the secure workspace you used during the Qualifiers.

## Schedule

- Until June 12: Teams test their submission using the competition setup on their machine.
- June 12, 2017: Deadline for qualified teams to submit their entries for pre-competition dry-run testing, wherein the ARIAC competition controllers will test the submission on the competition machine.
- June 12-14, 2017: Dry-run testing and iteration with teams to help resolve issues with their entries.
- June 14, 2017 @ 11:59:59pm UTC-07:00: Deadline for final submissions from qualified teams.
- June 15, 2017: Smoke-testing of final submissions.
- June 19-20, 2017: Perform official competition runs.
- June 21, 2017: Announcement of competition results.