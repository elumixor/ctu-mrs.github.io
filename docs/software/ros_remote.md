---
layout: default
title: ROS remote
parent: Software
---

# Connecting to ROS core remotely

ROS allows multiple computers to communicate and share topics and services via a local network.
This feature is useful for remote testing and simulations, where different ROS nodes can run on multiple machines as if they were on a single computer.

## Server computer, a.k.a., "the robot"

Add following lines to **.bashrc**:
```bash
export ROS_MASTER_URI=http://localhost:11311
```

**Important** (skipping these steps may kill ROS on the robot if it disconnects from a wifi):

- Do NOT export `ROS_IP` to **.bashrc**.
- Remove the server's (the robot's) own hostname in `/etc/hosts` except of `127.0.1.1`.
  The top of the `/etc/hosts` file of robot with hostname `dog` and IP `192.168.69.123` should look like below.
  For correct functionality, only one instance of `192.168.69.123` can be present in `/etc/hosts`. 
  Duplicated instances for IP `192.168.69.123` are not allowed.
```bash
127.0.0.1 localhost
127.0.1.1 dog
192.168.69.123 dog
```

## Client computer, a.k.a., "the notebook"

Add following lines to **.bashrc**:
```bash
export ROS_MASTER_URI=http://<server-hostname>:11311
```

The `<server-hostname>` should be specified in `/etc/hosts` on the client's computer, and `<client-hostname>` should be specified on the server computer.
You should be able to ping one from another using just its hostname.

When finished, don't forget to comment or delete the configuration on the client.
Otherwise, ROS will not be able to start.

For more information, follow to [wiki.ros.org/ROS/Tutorials/MultipleMachines](http://wiki.ros.org/ROS/Tutorials/MultipleMachines).
