This page describes how to configure the process center simulation environment by selecting and placing sensors and a robot arm.

The entire trial configuration is typically comprised of two configuration files:

 -  the 'Trial configuration file' that details specifics of a particular trial of the competition, which users will not have control over, and
 -  the 'Competitor configuration file' that details the placement of objects that users have control over. 

# Competitor configuration file

As a competitor, you are allowed to select the quantity, type, and location of sensors.

Your choices must be written using the [YAML](http://yaml.org/) syntax in a configuration file. Here is an [example configuration file](https://bitbucket.org/osrf/ariac/src/e0e07547305d3beeac8b723813cc0b73269e354b/gear_example/config/sample_gear_conf.yaml?at=ariac_2017&fileviewer=file-view-default).

## How to add sensors

The configuration YAML file contains a list of sensors denoted by the ``sensors:`` tag. Each sensor should have a unique name followed by the type of sensor and the sensor's position and orientation.

Available sensor types include:

1. break_beam
1. proximity
1. logical_camera
1. laser_profiler

A sensor's position and orientation is specified in global coordinates using and XYZ vector and Euler angles (roll, pitch, yaw).

The following is the specification of one `break_beam` sensor


```
#!yaml
sensors:
  break_beam_1:
    type: break_beam
    pose:
      xyz: [1.6, 2.25, 0.95]
      rpy: [0, 0, 'pi']
```

The following is the specification of both a `break_beam` and `logical_camera` sensor.

```
#!yaml

sensors:
  break_beam_1:
    type: break_beam
    pose:
      xyz: [1.6, 2.25, 0.95]
      rpy: [0, 0, 'pi']
  logical_camera_1:
    type: logical_camera
    pose:
      xyz: [1.21816, 3, 2]
      rpy: ['-pi', 'pi/2', 0]
```

Initial positioning and joint states of the robot arm that is automatically included in the workcell environment is not under participants' control.


# Competition configuration file
Each trial of the competition is specified using a separate configuration file. During the competition, competitors will not have control over the settings in this configuration file. However, you may find that modifying the settings assists you during system development.

Various settings can be specified, including:

1. The parts specified in the orders.
1. The models on the conveyor belt (which parts, where, how many).
1. The models in each bin (which parts, the configuration).
1. Which parts are faulty parts.
1. What causes the second order to be announced.
1. Which parts are dropped.


There are also some features which have been specifically implemented for use in development. These include:

1. Automatically fill a kit tray with the kit specified in an order.
1. Spawn models in various reference frames.

Here is a [sample competition trial configuration file](https://bitbucket.org/osrf/ariac/src/211e92c7eba0c0e4f4f812f82729255d7b070ca4/osrf_gear/config/example_custom_config.yaml?at=ariac_2017&fileviewer=file-view-default) (based off `qual2a.yaml` and `qual3b.yaml`), which explains how you can modify all of the aforementioned settings.

## Improving real-time factor during development

The real-time factor of a scenario is impacted by the number of models in the environment.
For users experiencing low real-time factors, reducing the number of parts that are in the scenario will help.

- If, for example, you are focusing on grasping parts from the conveyor belt, you can set `insert_models_over_bins` to `false` to temporarily not spawn parts in the storage bins.
- If you are focusing on grasping parts from the bins, you can set `belt_population_cycles` to `0` to temporarily not spawn parts on the conveyor belt.
- If you are focusing on grasping parts from a particular bin, you can comment out the other bins listed in `models_over_bins` to temporarily not spawn them.
- If you are focusing on placing parts in a particular AGV, you can manually delete the other AGV from the environment when the scenario starts.