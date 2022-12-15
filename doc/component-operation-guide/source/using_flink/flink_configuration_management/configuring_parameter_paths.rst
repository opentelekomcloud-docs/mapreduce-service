:original_name: mrs_01_1565.html

.. _mrs_01_1565:

Configuring Parameter Paths
===========================

All parameters of Flink must be set on a client. The path of a configuration file is as follows: *Client installation path*\ **/Flink/flink/conf/flink-conf.yaml**.

.. note::

   -  You are advised to set the parameters in the format of *Key*\ **:** *Value* in the **flink-conf.yaml** configuration file on the client.

      Example: **taskmanager.heap.size: 1024mb**

      A space is required between *Key*\ **:** and *Value*.

   -  If parameters are modified in the Flink service configuration, you need to download and install the client again after the configuration is complete.
