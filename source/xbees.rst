XBees
=====

XBees wireless radio devices are used as a transparent serial device to transmit
MAVLink messages with the vehicle. In order to use them properly, new XBees
should be configured.

.. note::

   In the future, it may make sense to transition away from the XBees to using
   the mavros TCP forwarding feature to connect directly with QGroundControl
   over WiFi. However, the XBees are useful for debugging because mavros does
   not need to be running.

Configuration
-------------

Use the `XBee command reference`_ to determine how to properly set the following
settings:

DH, DL
   These specify the destination address, and should be set to the SH and SL
   values of the paired XBee.

BD
   This is the baud rate for the serial communication. Set to ``6`` (57600 baud).

.. _`XBee command reference`: http://examples.digi.com/wp-content/uploads/2012/07/XBee_ZB_ZigBee_AT_Commands.pdf
