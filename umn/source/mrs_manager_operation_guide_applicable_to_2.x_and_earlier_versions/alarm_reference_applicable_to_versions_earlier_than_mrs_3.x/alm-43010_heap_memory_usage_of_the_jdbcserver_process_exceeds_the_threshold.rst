:original_name: alm_43010.html

.. _alm_43010:

ALM-43010 Heap Memory Usage of the JDBCServer Process Exceeds the Threshold
===========================================================================

Description
-----------

The system checks the JDBCServer process status every 30 seconds. The alarm is generated when the heap memory usage of the JDBCServer process exceeds the threshold (90% of the maximum memory).

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
43010    Major          Yes
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

If the available JDBCServer process heap memory is insufficient, a memory overflow occurs and the service breaks down.

Possible Causes
---------------

The heap memory of the JDBCServer process is overused or the heap memory is inappropriately allocated.

Procedure
---------

#. Check the heap memory usage.

   a. Go to the cluster details page and choose **Alarms**.

   b. Select the alarm whose **Alarm ID** is **43010** and view the IP address and role name of the instance in **Location**.

   c. Choose **Components** > **Spark** > **Instance** > **JDBCServer** (IP address of the instance for which the alarm is generated) > **Customize** > **Heap Memory Statistics of the JDBCServer Process**. Click **OK** to view the heap memory usage.

   d. Check whether the heap memory usage of JDBCServer has reached the threshold (90% of the maximum heap memory).

      -  If yes, go to :ref:`1.e <alm_43010__en-us_topic_0191813931_li1011493181634>`.
      -  If no, go to :ref:`2 <alm_43010__en-us_topic_0191813931_li572522141314>`.

   e. .. _alm_43010__en-us_topic_0191813931_li1011493181634:

      Choose **Components** > **Spark** > **Service Configuration**. Set **Type** to **All** and choose **JDBCServer** > **Tuning**. Increase the value of the **SPARK_DRIVER_MEMORY** parameter as required.

   f. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_43010__en-us_topic_0191813931_li572522141314>`.

#. .. _alm_43010__en-us_topic_0191813931_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
