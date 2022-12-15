:original_name: alm_43013.html

.. _alm_43013:

ALM-43013 JDBCServer GC Time Exceeds the Threshold
==================================================

Description
-----------

The system checks the GC time of the JDBCServer process every 60 seconds. This alarm is generated when the detected GC time exceeds the threshold (12 seconds) for three consecutive times. You can change the threshold by choosing **System** > **Threshold Configuration** > **Service** > **Spark** > **JDBCServer GC Time** > **Total JDBCServer GC Time**. This alarm is cleared when the JDBCServer GC time is shorter than or equal to the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
43013    Major          Yes
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

If the GC time exceeds the threshold, JDBCServer may run in low performance.

Possible Causes
---------------

The heap memory of the JDBCServer process is overused or inappropriately allocated, causing frequent GC.

Procedure
---------

#. Check the GC time.

   a. Go to the cluster details page and choose **Alarms**.

   b. Select the alarm whose **Alarm ID** is **43013** and view the IP address and role name of the instance in **Location**.

   c. Choose **Components** > **Spark** > **Instance** > **JDBCServer** (IP address of the instance for which the alarm is generated) > **Customize** > **GC Time of the JDBCServer Process**. Click **OK** to view the GC time.

   d. Check whether the GC time of the JDBCServer process is longer than 12 seconds.

      -  If yes, go to :ref:`1.e <alm_43013__en-us_topic_0191813943_li1011493181634>`.
      -  If no, go to :ref:`2 <alm_43013__en-us_topic_0191813943_li572522141314>`.

   e. .. _alm_43013__en-us_topic_0191813943_li1011493181634:

      Choose **Components** > **Spark** > **Service Configuration**. Set **Type** to **All** and choose **JDBCServer** > **Tuning**. Increase the value of the **SPARK_DRIVER_MEMORY** parameter as required.

   f. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_43013__en-us_topic_0191813943_li572522141314>`.

#. .. _alm_43013__en-us_topic_0191813943_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
