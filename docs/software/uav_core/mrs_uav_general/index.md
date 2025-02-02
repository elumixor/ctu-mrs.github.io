---
layout: default
title: mrs_uav_general
parent: uav_core
grand_parent: Software
---
# MRS UAV general

![](fig/thumbnail.jpg)

| Build status | [![Build Status](https://github.com/ctu-mrs/mrs_uav_general/workflows/Noetic/badge.svg)](https://github.com/ctu-mrs/mrs_uav_general/actions) |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------|

## Overview

This package contains configuration files, launch files, and utilities that are over-arching the packages in the [core](https://github.com/ctu-mrs/uav_core).

* **sensors.launch** - launches sensor drivers and produces static TFs based on the environment variables in the `.bashrc` (applies only for real UAVs)
* **core.launch** - launches the control pipeline, consisting of
  * [NodeletManager](https://github.com/ctu-mrs/mrs_uav_managers)
  * [ControlManager](https://github.com/ctu-mrs/mrs_uav_managers),
    * loads [controllers](https://github.com/ctu-mrs/mrs_uav_controllers)
    * loads [trackers](https://github.com/ctu-mrs/mrs_uav_trackers)
  * [UavManager](https://github.com/ctu-mrs/mrs_uav_managers)
  * [GainManager](https://github.com/ctu-mrs/mrs_uav_managers)
  * [ConstraintManager](https://github.com/ctu-mrs/mrs_uav_managers)
  * [Odometry](https://github.com/ctu-mrs/mrs_uav_odometry)
* **camera calibrations**
* **worlds** - definition of the safety areas and local gps system placement, used by [ControlManager](https://github.com/ctu-mrs/mrs_uav_managers) and [Odometry](https://github.com/ctu-mrs/mrs_uav_odometry)
* **automatic start** utility - triggers automatic takeoff after the uav is **arm** and successfully in **offboard**
  * disarms the UAV when pre-conditions are not met
  * can check for messages being published on topics specified in the [config file](https://github.com/ctu-mrs/mrs_uav_general/blob/master/config/automatic_start.yaml)
  * can trigger *user nodes* after takeoff via its `automatic_start/start` service (of type *std_srvs/Trigger*)
* **record.sh** script - generates and launches a launch file for recording rosbag (its simpler to add exclusions to this script)
