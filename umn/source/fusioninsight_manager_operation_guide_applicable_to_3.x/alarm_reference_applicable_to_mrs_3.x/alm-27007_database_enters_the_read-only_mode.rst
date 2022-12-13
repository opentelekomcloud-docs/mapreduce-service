:original_name: ALM-27007.html

.. _ALM-27007:

ALM-27007 Database Enters the Read-Only Mode
============================================

Description
-----------

The system checks the disk space usage of the data directory on the active DBServer node every 30 seconds. The alarm is generated when the disk space usage exceeds 90%.

The alarm is cleared when the disk space usage is lower than 80%.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
27007    Critical       Yes
======== ============== ==========

Parameters
----------

+-------------------+-----------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                     |
+===================+=============================================================================================================================+
| ClusterName       | Specifies the cluster for which the alarm is generated.                                                                     |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                     |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                        |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the actual indicator value exceeds this threshold, the alarm is generated. |
+-------------------+-----------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

The database enters the read-only mode, causing service data loss.

Possible Causes
---------------

The disk configuration cannot meet service requirements. The disk usage reaches the upper limit.

Procedure
---------

**Check whether the disk space usage reaches the upper limit.**

#. On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **DBService**.

#. On the **Dashboard** page, view the **Disk Space Usage of the Data Directory** chart and check whether the disk space usage of the data directory exceeds 90%.

   -  If yes, go to :ref:`3 <alm-27007__li203461531006>`.
   -  If no, go to :ref:`13 <alm-27007__li133383310015>`.

#. .. _alm-27007__li203461531006:

   Log in to the active management node of the DBServer as user **omm** and run the following commands to check whether the database enters the read-only mode:

   **source $DBSERVER_HOME/.dbservice_profile**

   **gsql -U omm -W** *password* **-d postgres -p 20051**

   **show default_transaction_read_only;**

   .. note::

      In the preceding commands, *password* indicates the password of user **omm** of the DBService database. You can run the **\\q** command to exit the database.

   Check whether the value of **default_transaction_read_only** is **on**.

   .. code-block:: text

      POSTGRES=# show default_transaction_read_only;
       default_transaction_read_only
      -------------------------------
       on
      (1 row)

   -  If yes, go to :ref:`4 <alm-27007__li1234615311708>`.
   -  If no, go to :ref:`13 <alm-27007__li133383310015>`.

#. .. _alm-27007__li1234615311708:

   Run the following commands to open the **dbservice.properties** file:

   **source $DBSERVER_HOME/.dbservice_profile**

   **vi ${DBSERVICE_SOFTWARE_DIR}/tools/dbservice.properties**

#. Change the value of **gaussdb_readonly_auto** to **OFF**.

#. Run the following command to open the **postgresql.conf** file:

   **vi ${DBSERVICE_DATA_DIR**}\ **/postgresql.conf**

#. Delete **default_transaction_read_only = on**.

#. Run the following command for the configuration to take effect:

   **gs_ctl reload -D ${DBSERVICE_DATA_DIR**}

#. Log in to FusionInsight Manager and choose **O&M** > **Alarm** > **Alarms**. On the right of the alarm "Database Enters the Read-Only Mode", click **Clear** in the **Operation** column. In the dialog box that is displayed, click **OK** to manually clear the alarm.

#. Log in to the active management node of the DBServer as user **omm** and run the following commands to view the files whose size exceeds 500 MB in the data directory and check whether there are large files incorrectly written into the directory:

   **source $DBSERVER_HOME/.dbservice_profile**

   **find "$DBSERVICE_DATA_DIR"/../ -type f -size +500M**

   -  If yes, go to :ref:`11 <alm-27007__li534815311101>`.
   -  If no, go to :ref:`13 <alm-27007__li133383310015>`.

#. .. _alm-27007__li534815311101:

   Handle the files that are incorrectly written into the directory based on the actual scenario.

#. Log in to FusionInsight Manager and choose **Cluster** > *Name of the desired cluster* > **Services** > **DBService**. On the **Dashboard** page, view the **Disk Space Usage of the Data Directory** chart and check whether the disk space usage is lower than 80%.

   -  If yes, no further action is required.
   -  If no, go to :ref:`13 <alm-27007__li133383310015>`.

**Collect fault information.**

13. .. _alm-27007__li133383310015:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

14. Expand the **Service** drop-down list, and select **DBService** for the target cluster.

15. Specify the host for collecting logs by setting the **Host** parameter which is optional. By default, all hosts are selected.

16. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

17. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269624001.png
