Running Experiments
===================

.. warning::

   Before running experiments, always verify that the vehicle is :doc:`set up
   <setup>` correctly.

Initializing the System
-----------------------

First, reload the `udev` service to ensure the Xtion is detected correctly::

   sudo service udev reload

Next, power cycle the flight control board to reinitialize (at least) the
position estimate. Now, for some mysterious reason, it is necessary to send some
data over the serial device before connecting with mavros. So, send a single
space with::

   screen /dev/ttyACM0

Now, start the ROS stack::

   roslaunch qex quad.launch

Before starting RGBDSLAMv2 make sure to align the camera to face perfectly
north. This is necessary to ensure the PX4 and ROS coordinate frames line up.
You can visualize the `fcu` transformation to verify the direction. Then, start
RGBDSLAMv2::

   rosservice call /Q1/rgbdslam/ros_ui_b pause false

Connecting Remotely
-------------------

There are two things you should be remotely connected to for running
experiments. On a remote computer, you should be connected to the flight control
board and to the onboard computer's ROS.

To connect to the flight control board, use the :doc:`xbees` as a serial link
for `QGroundControl`_.

.. _QGroundControl: http://www.qgroundcontrol.org/

To connect to ROS, follow the `ROS Network Setup Guide`_. The quadcopters
self-assign their IP addresses to ``192.168.0.9`` and ``192.168.0.10``. It may
be useful to add these to your :file:`/etc/hosts` file for easier use.

.. _ROS Network Setup Guide: http://wiki.ros.org/ROS/NetworkSetup/

.. note::

   Initial tests were conducted with the OSU Aerial Robotics Team router. The
   vehicles will not be able to assign their own IP addresses on OSU networks
   (``OSU_Secure``, etc.), so another router will need to be used.

Flying
------

Currently, there is no support for auto takeoff and landing. So, begin by arming
the vehicle by moving the throttle stick to the bottom right.

Next, raise the throttle to take off. Once the vehicle is stable and has reached
a safe altitude, use the ``OFFBOARD`` switch to transition to autonomous control.
