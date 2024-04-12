:original_name: mrs_01_1789.html

.. _mrs_01_1789:

Why Does It Take a Long Time to Run a Task Upon ResourceManager Active/Standby Switchover?
==========================================================================================

Question
--------

MapReduce job takes a very long time (more than 10minutes) when the ResourceManager switch while the job is running.

Answer
------

This is because, ResorceManager HA is enabled but the ResourceManager work preserving restart is not enabled.

If ResorceManager work preserving restart is not enabled, then ResorceManager switch containers are killed which causes the ResorceManager to timeout the ApplicationMaster. For details about the Work-preserving RM restart function, visit the following website:

Versions earlier than MRS 3.2.0: http://hadoop.apache.org/docs/r3.1.1/hadoop-yarn/hadoop-yarn-site/ResourceManagerRestart.html

MRS 3.2.0 or later: https://hadoop.apache.org/docs/r3.3.1/hadoop-yarn/hadoop-yarn-site/ResourceManagerRestart.html

The following method can be used to solve the issue:

Enable the ResorceManager work preserving restart feature by configuring the following parameter.

**yarn.resourcemanager.work-preserving-recovery.enabled**\ =\ **true**
