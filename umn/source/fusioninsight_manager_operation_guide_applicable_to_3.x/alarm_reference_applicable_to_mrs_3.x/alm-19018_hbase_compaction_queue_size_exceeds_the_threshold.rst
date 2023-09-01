:original_name: ALM-19018.html

.. _ALM-19018:

ALM-19018 HBase Compaction Queue Size Exceeds the Threshold
===========================================================

Description
-----------

The system checks the HBase compaction queue size every 300 seconds. This alarm is generated when the compaction queue size exceeds the alarm threshold (**100** by default). This alarm is cleared when the compaction queue size is less than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
19018    Minor          Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The cluster performance may deteriorate, affecting data read and write.

Possible Causes
---------------

-  The number of HBase RegionServers is too small.
-  There are excessive regions on a single RegionServer of HBase.
-  The HBase RegionServer heap size is small.
-  Resources are insufficient.
-  Related parameters are not configured properly.

Procedure
---------

**Check whether related parameters are properly configured.**

#. Log in to FusionInsight Manager and choose **O&M** > **Alarm** > **Alarms**. On the page that is displayed, check whether the alarm whose **Alarm ID** is **19008** or **19011** exists.

   -  If yes, click **View Help** next to the alarm and rectify the fault by referring to the help document. Then, go to :ref:`3 <alm-19018__li5814142393624>`.
   -  If no, go to :ref:`2 <alm-19018__li1681162011376>`.

#. .. _alm-19018__li1681162011376:

   On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase**. On the page that is displayed, click the **Configuration** tab then the **All Configurations** sub-tab, search for **hbase.hstore.compaction.min**, **hbase.hstore.compaction.max**, **hbase.regionserver.thread.compaction.small**, and **hbase.regionserver.thread.compaction.throttle**, and set them to larger values.

#. .. _alm-19018__li5814142393624:

   Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-19018__li5351076393624>`.

**Collect the fault information.**

4. .. _alm-19018__li5351076393624:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

5. Expand the **Service** drop-down list, and select **HBase** for the target cluster.

6. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767650.png
