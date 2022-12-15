:original_name: alm_43008.html

.. _alm_43008:

ALM-43008 Direct Memory Usage of the JobHistory Process Exceeds the Threshold
=============================================================================

Description
-----------

The system checks the JobHistory process status every 30 seconds. The alarm is generated when the direct memory usage of the JobHistory process exceeds the threshold (90% of the maximum memory).

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
43008    Major          Yes
======== ============== =====================

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

If the available JobHistory process direct memory is insufficient, a memory overflow occurs and the service breaks down.

Possible Causes
---------------

The direct memory of the JobHistory process is overused or the direct memory is inappropriately allocated.

Procedure
---------

#. Check the direct memory usage.

   a. Go to the cluster details page and choose **Alarms**.

   b. Select the alarm whose **Alarm ID** is **43008** and view the IP address and role name of the instance in **Location**.

   c. Choose **Components** > **Spark** > **Instance** > **JobHistory** (IP address of the instance for which the alarm is generated) > **Customize** > **Direct Memory Statistics of the JobHistory Process**. Click **OK** to view the direct memory usage.

   d. Check whether the direct memory usage of the JobHistory process has reached the threshold (90% of the maximum direct memory).

      -  If yes, go to :ref:`1.e <alm_43008__en-us_topic_0191813884_li1011493181634>`.
      -  If no, go to :ref:`2 <alm_43008__en-us_topic_0191813884_li572522141314>`.

   e. .. _alm_43008__en-us_topic_0191813884_li1011493181634:

      Choose **Components** > **Spark** > **Service Configuration**. Set **Type** to **All** and choose **JobHistory** > **Default**. Increase the value of **-XX:MaxDirectMemorySize** in **SPARK_DAEMON_JAVA_OPTS** as required.

   f. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_43008__en-us_topic_0191813884_li572522141314>`.

#. .. _alm_43008__en-us_topic_0191813884_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
