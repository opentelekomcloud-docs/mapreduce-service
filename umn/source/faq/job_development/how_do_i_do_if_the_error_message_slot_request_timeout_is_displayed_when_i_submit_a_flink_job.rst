:original_name: mrs_03_1237.html

.. _mrs_03_1237:

How Do I Do If the Error Message "slot request timeout" Is Displayed When I Submit a Flink Job?
===============================================================================================

Symptom
-------

When a Flink job is submitted, JobManager is started successfully. However, TaskManager remains in the starting state until timeout. The following error information is displayed:

.. code-block::

   org.apache.flink.runtime.jobmanager.scheduler.NoResourceAvailableException: Could not allocate the required slot within slot request timeout. Please make sure that the cluster has enough resources

Possible Causes
---------------

#. The resources in the YARN queue are insufficient. As a result, TaskManager fails to start.
#. Your JAR files conflict with those in the environment. You can execute the WordCount program to determine whether the issue occurs.
#. If the cluster is in security mode, the SSL certificate of Flink may be incorrectly configured or has expired.

Solution
--------

#. Add resources to the YARN queue.
#. Exclude the Flink and Hadoop dependencies in your JAR files so that Flink and Hadoop can depend only on the JAR files in the environment.
#. Reconfigure the SSL certificate of Flink..
