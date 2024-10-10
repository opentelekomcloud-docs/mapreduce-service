:original_name: mrs_08_0150.html

.. _mrs_08_0150:

JobGateway Basic Principles
===========================

JobGateway allows you to submit jobs through REST APIs.

As a gateway component for submitting big data jobs, JobGateway provides fully controllable enterprise-level big data job submission services, such as Spark, HBase, Flink, and Hive.

JobGateway Architecture
-----------------------

JobGateway consists of JobServer and JobBalancer instances.

-  JobBalancer provides load balancing.
-  JobServer provides REST APIs for submitting jobs.


.. figure:: /_static/images/en-us_image_0000001971163390.png
   :alt: **Figure 1** JobGateway architecture

   **Figure 1** JobGateway architecture
