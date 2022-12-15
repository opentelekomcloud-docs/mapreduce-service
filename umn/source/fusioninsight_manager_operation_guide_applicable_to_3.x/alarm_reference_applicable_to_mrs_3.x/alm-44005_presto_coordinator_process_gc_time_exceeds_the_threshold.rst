:original_name: ALM-44005.html

.. _ALM-44005:

ALM-44005 Presto Coordinator Process GC Time Exceeds the Threshold
==================================================================

Description
-----------

The system collects GC time of the Presto Coordinator process every 30 seconds. This alarm is generated when the GC time exceeds the threshold (exceeds 5 seconds for three consecutive times). You can change the threshold by choosing **System** > **Configure Alarm Threshold** > **Service** > **Presto** > **Coordinator** > **Presto Process Garbage Collection Time** > **Garbage Collection Time of the Coordinator Process** on MRS Manager. This alarm is cleared when the Coordinator process GC time is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
44005    Major          Yes
======== ============== ==========

Parameter
---------

=========== =========================================
Parameter   Description
=========== =========================================
ServiceName Service for which the alarm is generated.
RoleName    Role for which the alarm is generated.
HostName    Host for which the alarm is generated.
=========== =========================================

Impact on the System
--------------------

If the GC time of the Coordinator process is too long, the Coordinator process running performance will be affected and the Coordinator process will even be unavailable.

Possible Causes
---------------

The heap memory of the Coordinator process is overused or inappropriately allocated, causing frequent occurrence of the GC process.

Procedure
---------

#. Check the GC time.

   a. Go to the cluster details page and choose **Alarms**.

      .. note::

         For MRS 1.8.10 or earlier, log in to MRS Manager and choose **Alarms**.

   b. Select the alarm whose **Alarm ID** is **44005** and then check the role name in **Location** and confirm the IP adress of the instance.

   c. Choose **Components** > **Presto** > **Instances** > **Coordinator** (business IP address of the instance for which the alarm is generated) > **Customize** > **Presto Garbage Collection Time**. Click **OK** to view the GC time.

   d. Check whether the GC time of the Coordinator process is longer than 5 seconds.

      -  If yes, go to :ref:`1.e <alm-44005__en-us_topic_0225312712_li1011493181634>`.
      -  If no, go to :ref:`2 <alm-44005__en-us_topic_0225312712_li572522141314>`.

   e. .. _alm-44005__en-us_topic_0225312712_li1011493181634:

      Choose **Components** > **Presto** > **Service Configuration**, and switch **Basic** to **All**. Choose **Presto** > **Coordinator**. Increase the value of **-Xmx** (maximum heap memory) in the **JAVA_OPTS** parameter based on the site requirements.

   f. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm-44005__en-us_topic_0225312712_li572522141314>`.

#. .. _alm-44005__en-us_topic_0225312712_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.

   b. Call the OTC Customer Hotline for support.

      Germany: 0800 330 44 44

      International: +800 44556600

Reference
---------

None
