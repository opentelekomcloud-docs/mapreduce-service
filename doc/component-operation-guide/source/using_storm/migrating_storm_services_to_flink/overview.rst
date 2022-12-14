:original_name: mrs_01_1049.html

.. _mrs_01_1049:

Overview
========

This section applies to MRS 3.\ *x* or later.

From 0.10.0, Flink provides a set of APIs to smoothly migrate services compiled using Storm APIs to the Flink platform. This can be used in most of the service scenarios.

Flink supports the following service migration modes:

#. Complete migration of Storm services: Convert and run a complete Storm topology developed by Storm APIs.
#. Embedded migration of Storm services: Storm code is embedded in DataStream of Flink, for example, Spout/Bolt compiled using Storm APIs.

Flink provides the flink-storm package for the preceding service migration.
