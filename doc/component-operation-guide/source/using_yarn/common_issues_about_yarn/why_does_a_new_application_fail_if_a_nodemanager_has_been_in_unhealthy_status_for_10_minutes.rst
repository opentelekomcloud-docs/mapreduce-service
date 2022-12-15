:original_name: mrs_01_2085.html

.. _mrs_01_2085:

Why Does a New Application Fail If a NodeManager Has Been in Unhealthy Status for 10 Minutes?
=============================================================================================

Question
--------

Why does a new application fail if a NodeManager has been in unhealthy status for 10 minutes?

Answer
------

When **nodeSelectPolicy** is set to **SEQUENCE** and the first NodeManager connected to the ResourceManager is unavailable, the ResourceManager attempts to assign tasks to the same NodeManager in the period specified by **yarn.nm.liveness-monitor.expiry-interval-ms**.

You can use either of the following methods to avoid the preceding problem:

-  Use another nodeSelectPolicy, for example, **RANDOM**.

-  Go to the **All Configurations** page of Yarn by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_2125>`. Search for the following parameters in the search box and modify the following attributes in the **yarn-site.xml** file:

   **yarn.resourcemanager.am-scheduling.node-blacklisting-enabled** = **true**;

   **yarn.resourcemanager.am-scheduling.node-blacklisting-disable-threshold** = **0.5**.
