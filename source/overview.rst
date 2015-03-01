Overview
========

Before beginning development, you must understand the software environment
running on the vehicle. The entire software stack runs under `Robot Operating
System`_ (ROS). Within this system, a number of packages are used to enable certain
functionalites of the vehicle. Here is a visualization of these packages:

.. _Robot Operating System: http://ros.org

.. graphviz::

   digraph foo {
      rankdir="LR";

      node[shape="box", style=""];

      rgbdslam_v2 -> octomap -> frontier_exploration -> move_base -> mavros;
   }

The `RGBDSLAMv2`_ package takes RGB and depth images and localizes the vehicle
within its environment. We use it as the main source of localization on the
vehicle, and also to build a map of the environment.

The `OctoMap`_ package takes the point cloud as outputted from RGBDSLAMv2 and
turns it into a more usable format. It represents the world as a 3D
probabilistic occupancy grid. The probabilistic nature is good for us, because
it can handle changes in the environment (e.g. a person moving in and out of the
map).

`frontier_exploration`_ is used for exploring an unknown environment. Given an
occupancy map, it outputs boundaries between known and unknown regions
(frontiers). This technique allows the vehicle to exhaust unexplored regions
within its environment.

`move_base`_ accepts waypoints within the map and, using a cost map derived from
the occupancy map, plans a path around obstacles to arrive at the destination.
It outputs a velocity command which factors in the current location of the
vehicle to follow the path.

Finally, the `mavros`_ package allows for easy communication between ROS and the
flight controller. Specifically, it sends the RGBDSLAMv2 vision estimate to the
flight control board for sensor fusion, reads back the fused position estimate,
and sends velocity commands.

.. _RGBDSLAMv2: http://felixendres.github.io/rgbdslam_v2/
.. _OctoMap: https://octomap.github.io/
.. _frontier_exploration: http://wiki.ros.org/frontier_exploration/
.. _move_base: http://wiki.ros.org/move_base/
.. _mavros: https://github.com/mavlink/mavros/
