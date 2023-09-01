:original_name: ALM-19015.html

.. _ALM-19015:

ALM-19015 Quantity Quota Usage on ZooKeeper Exceeds the Threshold
=================================================================

Description
-----------

The system checks the ZNode usage of the HBase service every 120 seconds. This alarm is generated when the system detects that the ZNode quantity usage of the HBase service exceeds the alarm threshold (75% by default).

This alarm is cleared when the ZNode quantity usage is less than the alarm threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
19015    Major          Yes
======== ============== ==========

Parameters
----------

=========== =========================================================
Name        Meaning
=========== =========================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
Threshold   Specifies the threshold for which the alarm is generated.
=========== =========================================================

Impact on the System
--------------------

This alarm indicates that the ZNode quantity usage in the HBase service has exceeded the threshold. If this alarm is not handled in a timely manner, the problem severity may be escalated to **Critical**, affecting data writing.

Possible Causes
---------------

-  DR is configured for HBase, and data synchronization fails or is slow in DR.
-  A large number of WAL files are being split in the HBase cluster.

Procedure
---------

**Check the quantity quota and usage of ZNodes.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**, select the alarm whose ID is **19015**, and view the threshold in **Additional Information**.

#. Log in to the HBase client as user **root**. Run the following command to go to the client installation directory:

   **cd** *Client installation directory*

   Run the following command to set environment variables:

   **source bigdata_env**

   If the cluster uses the security mode, run the following command to perform security authentication:

   **kinit hbase**

   Enter the password as prompted (obtain the password from the MRS cluster administrator).

#. Run the **hbase zkcli** command to log in to the ZooKeeper client and run the **listquota /hbase** command to check the ZNode quantity quota of the HBase service. The ZNode root directory in the command is specified by the **zookeeper.znode.parent** parameter of the HBase service. The marked area in the following figure shows the quantity quota configuration of the root ZNode of the HBase service.

   |image1|

#. Run the **getusage /hbase/splitWAL** command to check the ZNode quantity usage and check whether the ratio of **Node count** in the command output to the ZNode quantity quota is close to the alarm threshold.

   -  If yes, go to :ref:`5 <alm-19015__li1269371131112>`.
   -  If no, go to :ref:`6 <alm-19015__li62018222616>`.

#. .. _alm-19015__li1269371131112:

   On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**. Check whether the alarm whose ID is **12007**, **19000**, or **19013** and the **ServiceName** in **Location** is the current HBase service exists.

   -  If yes, click **View Help** next to the alarm and rectify the fault by referring to the help document. Then, go to :ref:`8 <alm-19015__li9693191171112>`.
   -  If no, go to :ref:`9 <alm-19015__li146938101112>`.

#. .. _alm-19015__li62018222616:

   Run the **getusage /hbase/replication** command to check the ZNode quantity usage and check whether the ratio of **Node count** in the command output to the ZNode quantity quota is close to the alarm threshold.

   -  If yes, go to :ref:`7 <alm-19015__li17555915687>`.
   -  If no, go to :ref:`9 <alm-19015__li146938101112>`.

#. .. _alm-19015__li17555915687:

   On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**. Check whether the alarm whose ID is **19006** and **ServiceName** in **Location** is the current HBase service exists.

   -  If yes, click **View Help** next to the alarm and rectify the fault by referring to the help document. Then, go to :ref:`8 <alm-19015__li9693191171112>`.
   -  If no, go to :ref:`9 <alm-19015__li146938101112>`.

#. .. _alm-19015__li9693191171112:

   Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-19015__li146938101112>`.

**Collect the fault information.**

9.  .. _alm-19015__li146938101112:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

10. Expand the **Service** drop-down list, and select **HBase** for the target cluster.

11. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927609.png
.. |image2| image:: /_static/images/en-us_image_0000001532448238.png
