Setup
=====

Before conducting experiments, a few things should be checked.

PX4 Firmware
------------

We use a `custom branch`_ of the PX4 firmware available. This branch has a few
changes to support our setup:

.. _custom branch: https://github.com/osurdml/Firmware

* ARMv7M stack checks are enabled to solve SD card mounting issues on the
  PX4FMUv1 per `issue #1691`_.
* The external HMC5883 digital compass has been moved to a different I2C
  address.
* The PX4Flow module has been enabled.

.. _issue #1691: https://github.com/PX4/Firmware/issues/1691

Sensor Calibration
------------------

Use QGroundControl to recalibrate the accelerometer, gyroscope, and magnetometer
if strange behavior is exhibited. Note that some of these sensors are affected
by temperature, so may need to be recalibrated depending on the environment.

PX4 Parameters
--------------

PX4 maintains a list of parameters onboard the flight controller. The latest
parameters are stored at `osurdml/quadconf`_ in a text file that can be imported
from QGroundControl.

Here are some parameters that may need to be tuned depending on the application:

INAV_W_XY_*
   These parameters dictate the weighting of sensor sources. These will need to
   be adjusted depending on the sensors used.

MC_*_{P,I,D}
   These are the attitude controller PID gains. They may need to be adjusted for
   various payloads.

MPC_*_{P,I,D}
   These are the position controller PID gains.

.. _`osurdml/quadconf`: https://github.com/osurdml/quadconf
