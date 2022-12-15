:original_name: alm_14011.html

.. _alm_14011:

ALM-14011 HDFS DataNode Data Directory Is Not Configured Properly
=================================================================

Description
-----------

The DataNode parameter **dfs.datanode.data.dir** specifies the DataNode data directory. This alarm is generated in any of the following scenarios:

-  A configured data directory cannot be created.
-  A data directory uses the same disk as other critical directories in the system.
-  Multiple directories use the same disk.

This alarm is cleared when the DataNode data directory is configured properly and this DataNode is restarted.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14011    Major          Yes
======== ============== ==========

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

If the DataNode data directory is mounted on critical directories such as the root directory, the disk space of the root directory will be used up after running for a long time. This causes a system fault.

If the DataNode data directory is not configured properly, HDFS performance will deteriorate.

Possible Causes
---------------

-  The DataNode data directory fails to be created.
-  The DataNode data directory uses the same disk as critical directories, such as **/** or **/boot**.
-  Multiple directories in the DataNode data directory use the same disk.

Procedure
---------

#. Check the alarm cause and information about the DataNode for which the alarm is generated.

   a. On the MRS cluster details page, click **Alarms**. In the alarm list, click the alarm.
   b. In the **Alarm Details** area, view **Alarm Cause** to obtain the cause of the alarm. In **HostName** of **Location**, obtain the host name of the DataNode for which the alarm is generated.

#. Delete directories that do not comply with the disk plan from the DataNode data directory.

   a. Choose **Components** > **HDFS** > **Instances**. In the instance list, click the DataNode instance on the node for which the alarm is generated.

   b. Click **Instance Configuration** and view the value of the DataNode parameter **dfs.datanode.data.dir**.

   c. Check whether all DataNode data directories are consistent with the disk plan.

      -  If yes, go to :ref:`2.d <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_alm14011_mmccppss_s6>`.
      -  If no, go to :ref:`2.g <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s9>`.

   d. .. _alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_alm14011_mmccppss_s6:

      Modify the DataNode parameter **dfs.datanode.data.dir** and delete the incorrect directories.

   e. Choose **Components** > **HDFS** > **Instances** to restart the DataNode instance.

   f. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.g <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s9>`.

   g. .. _alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s9:

      Log in to the DataNode for which the alarm is generated.

      -  If the alarm cause is "The DataNode data directory fails to be created", go to :ref:`3.a <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_alm14011_mmccppss_s10>`.
      -  If the alarm cause is "The DataNode data directory uses the same disk as critical directories, such **/** or **/boot**", go to :ref:`4.a <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s16>`.
      -  If the alarm cause is "Multiple directories in the DataNode data directory use the same disk", go to :ref:`5.a <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s20>`.

#. Check whether the DataNode data directory fails to be created.

   a. .. _alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_alm14011_mmccppss_s10:

      Run the following commands to switch the user:

      **sudo su - root**

      **su - omm**

   b. Run the **ls** command to check whether the directories exist in the DataNode data directory.

      -  If yes, go to :ref:`7 <alm_14011__en-us_topic_0191813967_li572522141314>`.
      -  If no, go to :ref:`3.c <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_alm14011_mmccppss_s12>`.

   c. .. _alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_alm14011_mmccppss_s12:

      Run the **mkdir** *data directory* command to create a directory and check whether the directory is successfully created.

      -  If yes, go to :ref:`6.a <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s23>`.
      -  If no, go to :ref:`3.d <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s1233>`.

   d. .. _alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s1233:

      Click **Alarms** to check whether alarm ALM-12017 Insufficient Disk Capacity exists.

      -  If yes, go to :ref:`3.e <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s154>`.
      -  If no, go to :ref:`3.f <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_alm14011_mmccppss_s13>`.

   e. .. _alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s154:

      Adjust the disk capacity and check whether alarm ALM-12017 Insufficient Disk Capacity is cleared. For details, see :ref:`ALM-12017 Insufficient Disk Capacity <alm_12017>`.

      -  If yes, go to :ref:`ALM-12017 Insufficient Disk Capacity <alm_12017>`.
      -  If no, go to :ref:`7 <alm_14011__en-us_topic_0191813967_li572522141314>`.

   f. .. _alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_alm14011_mmccppss_s13:

      Check whether user **omm** has the **rwx** or **x** permission of all the upper-layer directories of the directory. (For example, for **/tmp/abc/**, user **omm** has the **x** permission for directory **tmp** and the **rwx** permission for directory **abc**.)

      -  If yes, go to :ref:`6.a <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s23>`.
      -  If no, go to :ref:`3.g <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s14>`.

   g. .. _alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s14:

      Run the **chmod u+rwx** *path* or **chmod u+x** *path* command as the **root** user to add the **rwx** or **x** permission to the paths. Then, go to :ref:`3.c <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_alm14011_mmccppss_s12>`.

#. Check whether the DataNode data directory uses the same disk as other critical directories in the system.

   a. .. _alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s16:

      Run the **df** command to obtain the disk mounting information of each directory in the DataNode data directory.

   b. Check whether the directories mounted to the disk are critical directories, such as **/** or **/boot**.

      -  If yes, go to :ref:`4.c <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s18>`.
      -  If no, go to :ref:`6.a <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s23>`.

   c. .. _alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s18:

      Change the value of the DataNode parameter **dfs.datanode.data.dir** and delete the directories that use the same disk as critical directories.

   d. Go to :ref:`6.a <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s23>`.

#. Check whether multiple directories in the DataNode data directory use the same disk.

   a. .. _alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s20:

      Run the **df** command to obtain the disk mounting information of each directory in the DataNode data directory. Record the mounted directory in the command output.

   b. Modify the DataNode node parameter **dfs.datanode.data.dir** to reserve one of the directories mounted on the same disk directory.

   c. Go to :ref:`6.a <alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s23>`.

#. Restart the DataNode and check whether the alarm is cleared.

   a. .. _alm_14011__en-us_topic_0191813967_en-us_topic_0035998730_s23:

      Choose **Components** > **HDFS** > **Instances** to restart the DataNode instance.

   b. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`7 <alm_14011__en-us_topic_0191813967_li572522141314>`.

#. .. _alm_14011__en-us_topic_0191813967_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
