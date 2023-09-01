:original_name: ALM-45641.html

.. _ALM-45641:

ALM-45641 Data Synchronization Exception Between the Active and Standby FlinkServer Nodes
=========================================================================================

This section applies to MRS 3.2.0 or later.

Description
-----------

The system checks data synchronization between the active and standby FlinkServer nodes every 60 seconds. This alarm is generated when the standby FlinkServer node fails to synchronize files with the active FlinkServer node.

This alarm is cleared when the standby FlinkServer synchronizes files with the active FlinkServer.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45641    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

Because the configuration files on the standby FlinkServer are not updated, some configurations will be lost after an active/standby switchover. FlinkServer and some components may not run properly.

Possible Causes
---------------

-  The link between the active and standby FlinkServer nodes is interrupted.
-  The synchronization file does not exist or the file permission is required.

Procedure
---------

**Check whether the network between the active and standby FlinkServer is in normal state.**

#. On FusionInsight Manager, choose **Cluster** > **Services** > **ClickHouse** > **Instance**. View and record the IP addresses of active and standby FlinkServer.

#. Log in to the active FlinkServer node as the **root** user.

#. Run the following command to check whether the standby FlinkServer is reachable:

   **ping** *IP address of the standby FlinkServer*

   -  If yes, go to :ref:`6 <alm-45641__li18750195794719>`.
   -  If no, go to :ref:`4 <alm-45641__li63406959171631>`.

#. .. _alm-45641__li63406959171631:

   Contact the network administrator to check whether the network is faulty.

   -  If yes, go to :ref:`5 <alm-45641__li19595462171631>`.
   -  If no, go to :ref:`6 <alm-45641__li18750195794719>`.

#. .. _alm-45641__li19595462171631:

   Rectify the network fault and check whether the alarm is cleared from the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45641__li18750195794719>`.

**Check whether the storage space of the /srv/BigData/LocalBackup directory is full.**

6. .. _alm-45641__li18750195794719:

   Run the following command to check whether the storage space of the **/srv/BigData/LocalBackup** directory is full:

   **df -hl /srv/BigData/LocalBackup**

   -  If yes, go to :ref:`7 <alm-45641__li7740734122412>`.
   -  If no, go to :ref:`10 <alm-45641__li13330195272015>`.

7. .. _alm-45641__li7740734122412:

   Run the following command to clear unnecessary backup files:

   **rm -rf** *Directory to be cleared*

   The following are two examples:

   **rm -rf** **/srv/BigData/LocalBackup/0/default-oms_20191211143443**

8. On FusionInsight Manager, choose **O&M** > **Backup and Restoration** > **Backup Management**.

   In the **Operation** column of the backup task, click **Configure** and change the value of **Maximum Number of Backup Copies** to reduce the number of backup file sets.

9. Wait for 1 minute and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-45641__li13330195272015>`.

**Check whether the synchronization file exists and whether the file permission is valid.**

10. .. _alm-45641__li13330195272015:

    Run the following command to check whether the synchronization file exists:

    **find /srv/BigData/ -name "sed*"**

    **find /opt -name "sed*"**

    -  If yes, go to :ref:`11 <alm-45641__li6383747162115>`.
    -  If no, go to :ref:`12 <alm-45641__li210153713915>`.

11. .. _alm-45641__li6383747162115:

    Run the following command to check the synchronization file information and permission queried in :ref:`10 <alm-45641__li13330195272015>`:

    **ll** *Path of the file you want to search for*

    -  If the file size is 0 and all values in the permission column are -, the file is a junk file. Run the following command to delete it:

       **rm -rf** *Files to be deleted*

       Wait for several minutes and check whether the alarm is cleared. If the alarm persists, go to :ref:`12 <alm-45641__li210153713915>`.

    -  If the file size is not 0, go to :ref:`12 <alm-45641__li210153713915>`.

12. .. _alm-45641__li210153713915:

    View the log file generated when the alarm is reported.

    a. Run the following command to go to the HA run log file path of the current cluster:

       **cd /var/log/Bigdata/flink/flinkserver/ha/runlog**

    b. Decompress log file and view the logs generated when the alarm is reported.

       For example, if the name of the file is **ha.log.2021-03-22_12-00-07.gz**, run the following command:

       **gunzip** *ha.log.2021-03-22_12-00-07.gz*

       **vi** *ha.log.2021-03-22_12-00-07*

       Check whether error information is displayed before and after the alarm generation time in the logs.

       -  If it is displayed, rectify the fault based on the error information. Go to :ref:`13 <alm-45641__li259318693811>`.

          For example, if the following error information is displayed, the directory permission is required. In this case, obtain the directory permission that is the same as the permission on a normal node.

          |image1|

       -  If no, go to :ref:`14 <alm-45641__li42141433171631>`.

13. .. _alm-45641__li259318693811:

    Wait for about 10 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-45641__li42141433171631>`.

**Collect fault information.**

14. .. _alm-45641__li42141433171631:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

15. Select FlinkServer information from **Services** and click **OK**.

16. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the hosts to which the role belongs, and click **OK**.

17. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

18. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767430.png
.. |image2| image:: /_static/images/en-us_image_0000001583127333.png
