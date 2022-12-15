:original_name: ALM-13005.html

.. _ALM-13005:

ALM-13005 Failed to Set the Quota of Top Directories of ZooKeeper Components
============================================================================

Description
-----------

The system sets quotas for each ZooKeeper top-level directory in the **customized.quota** configuration item and components every 5 hours. This alarm is generated when the system fails to set the quota for a directory.

This alarm is cleared when the setting succeeds after a failure.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
13005    Minor          Yes
======== ============== =====================

Parameters
----------

+-------------------+--------------------------------------------------------------+
| Name              | Meaning                                                      |
+===================+==============================================================+
| Source            | Specifies the cluster for which the alarm is generated.      |
+-------------------+--------------------------------------------------------------+
| ServiceName       | Specifies the service name for which the alarm is generated. |
+-------------------+--------------------------------------------------------------+
| ServiceDirectory  | Specifies the directory for which the alarm is generated.    |
+-------------------+--------------------------------------------------------------+
| Trigger Condition | Specifies the cause of the alarm.                            |
+-------------------+--------------------------------------------------------------+

Impact on the System
--------------------

Components can write a large amount of data to the top-level directory of ZooKeeper. As a result, the ZooKeeper service is unavailable.

Possible Causes
---------------

The quota for the alarm directory is inappropriate.

Procedure
---------

**Check whether the quota for the alarm directory is appropriate.**

#. Log in to FusionInsight Manager, and choose **Cluster >** *Name of the desired cluster* **> Services** > **ZooKeeper**. On the displayed page, choose **Configurations** > **All Configurations** > **Quota**. Check whether the directory for which the alarm is reported and its quota exist in the **customized.quota** configuration item.

   -  If yes, go to :ref:`5 <alm-13005__li38538052161727>`.
   -  If no, go to :ref:`2 <alm-13005__li8446514299>`.

#. .. _alm-13005__li8446514299:

   Check whether the alarm directory for which the alarm is reported is in the following alarm list.

   .. table:: **Table 1** Component alarm directory

      ========= ===============
      Component Alarm Directory
      ========= ===============
      Hbase     /hbase
      Hive      /beelinesql
      Yarn      /rmstore
      Storm     /stormroot
      Streaming /storm
      Kafka     /kafka
      ========= ===============

   -  If yes, go to :ref:`3 <alm-13005__li1454514461317>`.
   -  If no, go to :ref:`7 <alm-13005__li34986499161727>`.

#. .. _alm-13005__li1454514461317:

   View the component of the alarm directory in the table, open the corresponding service page, and choose **Configurations** > **All Configurations**. On the displayed page, search for **zk.quota** in the upper right corner. The search result is the quota of the alarm directory.

#. Check whether the quota of the alarm directory for which the alarm is reported is appropriate. The quota must be greater than or equal to the actual value, which can be obtained in **Trigger Condition**.

#. .. _alm-13005__li38538052161727:

   Modify the **services.quota** value as prompted and save the configuration.

#. After the time specified by **service.quotas.auto.check.cron.expression**, check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If no, go to :ref:`7 <alm-13005__li34986499161727>`.

**Collect fault information.**

7.  .. _alm-13005__li34986499161727:

    On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

8.  Select **ZooKeeper** in the required cluster from the **Service**.

9.  Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383946.png
