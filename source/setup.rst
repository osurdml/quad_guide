Setup
=====

Before conducting experiments, a few things should be checked.

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
