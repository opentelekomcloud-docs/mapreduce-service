:original_name: mrs_01_1010.html

.. _mrs_01_1010:

Configuring Region In Transition Recovery Chore Service
=======================================================

Scenario
--------

In a faulty environment, there are possibilities that a region may be stuck in transition for longer duration due to various reasons like slow region server response, unstable network, ZooKeeper node version mismatch. During region transition, client operation may not work properly as some regions will not be available.

Configuration
-------------

A chore service should be scheduled at HMaster to identify and recover regions that stay in the transition state for a long time.

The following table describes the parameters for enabling this function.

.. table:: **Table 1** Parameters

   +-----------------------------------------------+-----------------------------------------------------------------------------------------------+---------------+
   | Parameter                                     | Description                                                                                   | Default Value |
   +===============================================+===============================================================================================+===============+
   | hbase.region.assignment.auto.recovery.enabled | Configuration parameter used to enable/disable the region assignment recovery thread feature. | true          |
   +-----------------------------------------------+-----------------------------------------------------------------------------------------------+---------------+
