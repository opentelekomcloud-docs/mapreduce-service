:original_name: mrs_08_0098.html

.. _mrs_08_0098:

CDL Basic Principles
====================

Overview
--------

Change Data Loader (CDL) is a real-time data integration service based on Kafka Connect. The CDL service captures data change events from various OLTP databases and push them to Kafka. Then, Sink Connector pushes the events to the big data ecosystem.

Currently, CDL supports MySQL, PostgreSQL, Oracle, Hudi, Kafka, and ThirdParty-Kafka data sources. Data can be written to Kafka, Hudi, DWS, and ClickHouse.

CDL structure
-------------

The CDL service contains two important roles: CDLConnector and CDLService. CDLConnector, including Source Connector and Sink Connector, is the instance for executing data capture jobs. CDLService is the instance for managing and creating jobs.

|image1|

The CDLService instances of the CDL service work in multi-active mode. Any CDLService instance can perform service operations. The CDLConnector instances work in distributed mode and provide HA and rebalance capabilities. When tasks are created, the number of tasks specified is balanced among CDLConnector instances in a cluster to ensure that the number of tasks running on each instance is similar. If a CDLConnector instance is abnormal or a node breaks down, the number of tasks are rebalanced on other nodes.


.. figure:: /_static/images/en-us_image_0000001349190333.png
   :alt: **Figure 1** Rebalance of a task

   **Figure 1** Rebalance of a task

.. |image1| image:: /_static/images/en-us_image_0000001349309917.png
