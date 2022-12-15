:original_name: mrs_03_1229.html

.. _mrs_03_1229:

How Do I Do If the launcher-job Queue Is Stopped by YARN due to Insufficient Heap Size When I Submit a Flink Job on the Management Plane?
=========================================================================================================================================

Symptom
-------

The launcher-job queue is stopped by YARN when a Flink job is submitted on the management plane.

Solution
--------

Increase the heap size of the launcher-job queue.

#. Log in to the active OMS node as user **omm**.
#. Change the value of **job.launcher.resource.memory.mb** in **/opt/executor/webapps/executor/WEB-INF/classes/servicebroker.xml** to **2048**.
#. Run the **sh /opt/executor/bin/restart-executor.sh** command to restart the executor process.
