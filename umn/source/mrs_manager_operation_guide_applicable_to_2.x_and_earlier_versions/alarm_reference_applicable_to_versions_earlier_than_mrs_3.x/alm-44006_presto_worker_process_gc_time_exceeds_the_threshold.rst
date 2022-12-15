:original_name: alm_44006.html

.. _alm_44006:

ALM-44006 Presto Worker Process GC Time Exceeds the Threshold
=============================================================

Description
-----------

The system collects GC time of the Presto Worker process every 30 seconds. This alarm is generated when the GC time exceeds the threshold (exceeds 5 seconds for three consecutive times). You can change the threshold by choosing **System** > **Configure Alarm Threshold** > **Service** > **Presto** > **Worker** > **Presto Garbage Collection Time** > **Garbage Collection Time of the Worker Process** on MRS Manager. This alarm is cleared when the Worker process GC time is shorter than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
44006    Major          Yes
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

If the GC time of the Worker process is too long, the Worker process running performance will be affected and the Worker process will even be unavailable.

Possible Causes
---------------

The heap memory of the Worker process is overused or inappropriately allocated, causing frequent occurrence of the GC process.

Procedure
---------

#. Check the GC time.

   a. Go to the cluster details page and choose **Alarms**.

   b. Select the alarm whose **Alarm ID** is **44006**. Then check the IP address and role name of the instance in **Location**.

   c. Choose **Components** > **Presto** > **Instances** > **Worker** (business IP address of the instance for which the alarm is generated) > **Customize** > **Presto Garbage Collection Time**. Click **OK** to view the GC time.

   d. Check whether the GC time of the Worker process is longer than 5 seconds.

      -  If yes, go to :ref:`1.e <alm_44006__en-us_topic_0225312713_li3841416113916>`.
      -  If no, go to :ref:`2 <alm_44006__en-us_topic_0225312713_li572522141314>`.

   e. .. _alm_44006__en-us_topic_0225312713_li3841416113916:

      Choose **Components** > **Presto** > **Service Configuration**, and switch **Basic** to **All**, and choose **Presto** > **Worker** Increase the value of **-Xmx** (maximum heap memory) in the **JAVA_OPTS** parameter based on the site requirements.

   f. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_44006__en-us_topic_0225312713_li572522141314>`.

#. .. _alm_44006__en-us_topic_0225312713_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
