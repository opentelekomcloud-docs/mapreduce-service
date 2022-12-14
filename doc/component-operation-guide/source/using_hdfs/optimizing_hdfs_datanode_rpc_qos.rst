:original_name: mrs_01_1673.html

.. _mrs_01_1673:

Optimizing HDFS DataNode RPC QoS
================================

Scenario
--------

When the speed at which the client writes data to the HDFS is greater than the disk bandwidth of the DataNode, the disk bandwidth is fully occupied. As a result, the DataNode does not respond. The client can back off only by canceling or restoring the channel, which results in write failures and unnecessary channel recovery operations.

.. note::

   This section applies to MRS 3.\ *x* or later.

Configuration
-------------

The new configuration parameter **dfs.pipeline.ecn** is introduced. When this configuration is enabled, the DataNode sends a signal from the write channel when the write channel is overloaded. The client may perform backoff based on the blocking signal to prevent the system from being overloaded. This configuration parameter is introduced to make the channel more stable and reduce unnecessary cancellation or recovery operations. After receiving the signal, the client backs off for a period of time (5,000 ms), and then adjusts the backoff time based on the related filter (the maximum backoff time is 50,000 ms).

Go to the **All Configurations** page of HDFS and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`.

.. table:: **Table 1** DN ECN configuration

   +------------------+----------------------------------------------------------------------------------+---------------+
   | Parameter        | Description                                                                      | Default Value |
   +==================+==================================================================================+===============+
   | dfs.pipeline.ecn | After configuration, the DataNode can send blocking notifications to the client. | false         |
   +------------------+----------------------------------------------------------------------------------+---------------+
