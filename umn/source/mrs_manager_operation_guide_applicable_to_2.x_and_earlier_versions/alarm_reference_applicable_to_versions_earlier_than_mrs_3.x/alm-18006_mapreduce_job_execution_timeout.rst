:original_name: alm_18006.html

.. _alm_18006:

ALM-18006 MapReduce Job Execution Timeout
=========================================

Description
-----------

The alarm module checks the MapReduce job execution every 30 seconds. This alarm is generated when the execution of a submitted MapReduce job times out.

This alarm must be manually cleared.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
18006    Major          No
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------------------+
| Parameter         | Description                                                                         |
+===================+=====================================================================================+
| ServiceName       | Specifies the service for which the alarm is generated.                             |
+-------------------+-------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| Trigger condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

Execution of the submitted MapReduce job times out, so no execution result can be obtained. Execute the job again after rectifying the fault.

Possible Causes
---------------

It takes a long time to execute a MapReduce job. However, the specified time is less than the required execution time.

Procedure
---------

#. Check whether time is improperly set.

   Set **-Dapplication.timeout.interval** to a larger value, or do not set the parameter. Check whether the MapReduce job can be executed.

   -  If yes, go to :ref:`2.e <alm_18006__en-us_topic_0191813946_clean>`.
   -  If no, go to :ref:`2.b <alm_18006__en-us_topic_0191813946_substep_03d21a89>`.

#. Check the Yarn status.

   a. Go to the cluster details page and choose **Alarms**.

   b. .. _alm_18006__en-us_topic_0191813946_substep_03d21a89:

      In the alarm list on MRS Manager, check whether the alarm ALM-18000 Yarn Service Unavailable is generated.

      -  If yes, go to :ref:`2.c <alm_18006__en-us_topic_0191813946_substep_03d82569>`.
      -  If no, go to :ref:`3 <alm_18006__en-us_topic_0191813946_li12092809151957>`.

   c. .. _alm_18006__en-us_topic_0191813946_substep_03d82569:

      Rectify the fault by following the handling procedure in :ref:`ALM-18000 Yarn Service Unavailable <alm_18000>`.

   d. Run the MapReduce job command again to check whether the MapReduce job can be executed.

      -  If yes, go to :ref:`2.e <alm_18006__en-us_topic_0191813946_clean>`.
      -  If no, go to :ref:`4 <alm_18006__en-us_topic_0191813946_li572522141314>`.

   e. .. _alm_18006__en-us_topic_0191813946_clean:

      In the alarm list, click |image1| in the **Operation** column of the alarm to manually clear the alarm. No further action is required.

#. .. _alm_18006__en-us_topic_0191813946_li12092809151957:

   Adjust the timeout threshold.

   On MRS Manager, choose **System** > **Threshold Configuration** > **Services** > **Yarn** > **Timed out Applications**, and increase the maximum number of timeout tasks allowed by the current threshold rule. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm_18006__en-us_topic_0191813946_li572522141314>`.

#. .. _alm_18006__en-us_topic_0191813946_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None

.. |image1| image:: /_static/images/en-us_image_0000001349257373.png
