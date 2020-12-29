# Log files used during qualification tasks
Submissions for qualification tasks run "at home" require users to submit ARIAC log files.
Log files for each run are written to the `~/.ariac/log` directory. The following files are generated.

## 1. Task performance log file

The task performance log file is written to `~/.ariac/log/performance.log`.
This file will be reviewed to evaluate your performance in the task.

*Note: if you are using a gazebo port other than the default (11345), your task performance log file will be at `~/.gazebo/server-<port number>/default.log`.*

## 2. Simulation state log file

The simulation state log file is written to `~/.ariac/log/gazebo/state.log`.
This log stores all of the simulation data during the trial and may be used to confirm your task performance log file.


**Log files are over-written with every run or playback of the ARIAC software, so make a backup of your submission files before running more trials.** As the performance log is a symbolic link to another file, be sure to use the `cp --dereference` option when copying the `~/.ariac/log` directory.


# Playback of log files
It's highly recommended that you review your log files before submission, using:

```
roslaunch osrf_gear gear_playback.launch
# Or, if you want to specify a specific log file:
roslaunch osrf_gear gear_playback.launch state_log_path:=`pwd`/qual_2.log
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