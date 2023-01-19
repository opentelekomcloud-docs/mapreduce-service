:original_name: mrs_01_1664.html

.. _mrs_01_1664:

Changing the DataNode Storage Directory
=======================================

Scenario
--------

If the storage directory defined by the HDFS DataNode is incorrect or the HDFS storage plan changes, the system administrator needs to modify the DataNode storage directory on FusionInsight Manager to ensure that the HDFS works properly. Changing the ZooKeeper storage directory includes the following scenarios:

-  Change the storage directory of the DataNode role. In this way, the storage directories of all DataNode instances are changed.
-  Change the storage directory of a single DataNode instance. In this way, only the storage directory of this instance is changed, and the storage directories of other instances remain the same.

Impact on the System
--------------------

-  The HDFS service needs to be stopped and restarted during the process of changing the storage directory of the DataNode role, and the cluster cannot provide services before it is completely started.

-  The DataNode instance needs to stopped and restarted during the process of changing the storage directory of the instance, and the instance at this node cannot provide services before it is started.
-  The directory for storing service parameter configurations must also be updated.

Prerequisites
-------------

-  New disks have been prepared and installed on each data node, and the disks are formatted.

-  New directories have been planned for storing data in the original directories.
-  The HDFS client has been installed.
-  The system administrator user **hdfs** is available.
-  When changing the storage directory of a single DataNode instance, ensure that the number of active DataNode instances is greater than the value of **dfs.replication**.

Procedure
---------

**Check the environment.**

#. Log in to the server where the HDFS client is installed as user **root**, and run the following command to configure environment variables:

   **source** *Installation directory of the HDFS client*\ **/bigdata_env**

#. If the cluster is in security mode, run the following command to authenticate the user:

   **kinit hdfs**

#. Run the following command on the HDFS client to check whether all directories and files in the HDFS root directory are normal:

   **hdfs fsck /**

   Check the fsck command output.

   -  If the following information is displayed, no file is lost or damaged. Go to :ref:`4 <mrs_01_1664__en-us_topic_0000001219350541_le587d508c49b4837bcabd9bd9cf98bc4>`.

      .. code-block::

         The filesystem under path '/' is HEALTHY

   -  If other information is displayed, some files are lost or damaged. Go to :ref:`5 <mrs_01_1664__en-us_topic_0000001219350541_l1ce08f0a7d2349b487dd6f19c38c7273>`.

#. .. _mrs_01_1664__en-us_topic_0000001219350541_le587d508c49b4837bcabd9bd9cf98bc4:

   Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services**, and check whether **Running Status** of HDFS is **Normal**.

   -  If yes, go to :ref:`6 <mrs_01_1664__en-us_topic_0000001219350541_lff55f0ef8699449ab4cfc4eddeed1711>`.
   -  If no, the HDFS status is unhealthy. Go to :ref:`5 <mrs_01_1664__en-us_topic_0000001219350541_l1ce08f0a7d2349b487dd6f19c38c7273>`.

#. .. _mrs_01_1664__en-us_topic_0000001219350541_l1ce08f0a7d2349b487dd6f19c38c7273:

   Rectify the HDFS fault.. The task is complete.

#. .. _mrs_01_1664__en-us_topic_0000001219350541_lff55f0ef8699449ab4cfc4eddeed1711:

   Determine whether to change the storage directory of the DataNode role or that of a single DataNode instance:

   -  To change the storage directory of the DataNode role, go to :ref:`7 <mrs_01_1664__en-us_topic_0000001219350541_l4bc534684e1d4d3cb656e4ed55bb75af>`.
   -  To change the storage directory of a single DataNode instance, go to :ref:`12 <mrs_01_1664__en-us_topic_0000001219350541_lab34cabb4d324166acebeb18e1098884>`.

**Changing the storage directory of the DataNode role**

7.  .. _mrs_01_1664__en-us_topic_0000001219350541_l4bc534684e1d4d3cb656e4ed55bb75af:

    Choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **Stop Instance** to stop the HDFS service.

8.  Log in to each data node where the HDFS service is installed as user **root** and perform the following operations:

    a. Create a target directory (**data1** and **data2** are original directories in the cluster).

       For example, to create a target directory **${BIGDATA_DATA_HOME}/hadoop/data3/dn**, run the following commands:

       **mkdir** **${BIGDATA_DATA_HOME}/hadoop/data3** and **mkdir ${BIGDATA_DATA_HOME}/hadoop/data3/dn**

    b. Mount the target directory to the new disk. For example, mount **${BIGDATA_DATA_HOME}/hadoop/data3** to the new disk.

    c. Modify permissions on the new directory.

       For example, to create a target directory **${BIGDATA_DATA_HOME}/hadoop/data3/dn**, run the following commands:

       **chmod 700** **${BIGDATA_DATA_HOME}/hadoop/data3/dn -R** and **chown omm:wheel** **${BIGDATA_DATA_HOME}/hadoop/data3/dn -R**

    d. .. _mrs_01_1664__en-us_topic_0000001219350541_l63f4856203e9425f9a23113c3d13f665:

       Copy the data to the target directory.

       For example, if the old directory is **${BIGDATA_DATA_HOME}/hadoop/data1/dn** and the target directory is **${BIGDATA_DATA_HOME}/hadoop/data3/dn**, run the following command:

       **cp -af** **${BIGDATA_DATA_HOME}/hadoop/data1/dn/\*** **${BIGDATA_DATA_HOME}/hadoop/data3/dn**

9.  On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **Configurations** > **All Configurations** to go to the HDFS service configuration page.

    Change the value of **dfs.datanode.data.dir** from the default value **%{@auto.detect.datapart.dn}** to the new target directory, for example, **${BIGDATA_DATA_HOME}/hadoop/data3/dn**.

    For example, the original data storage directories are **/srv/BigData/hadoop/data1**, **/srv/BigData/hadoop/data2**. To migrate data from the **/srv/BigData/hadoop/data1** directory to the newly created **/srv/BigData/hadoop/data3** directory, replace the whole parameter with **/srv/BigData/hadoop/data2, /srv/BigData/hadoop/data3**. Separate multiple storage directories with commas (,). In this example, changed directories are **/srv/BigData/hadoop/data2**, **/srv/BigData/hadoop/data3**.

10. Click **Save**. Choose **Cluster** > *Name of the desired cluster* > **Services**. On the page that is displayed, start the services that have been stopped.

11. After the HDFS is started, run the following command on the HDFS client to check whether all directories and files in the HDFS root directory are correctly copied:

    **hdfs fsck /**

    Check the fsck command output.

    -  If the following information is displayed, no file is lost or damaged, and data replication is successful. No further action is required.

       .. code-block::

          The filesystem under path '/' is HEALTHY

    -  If other information is displayed, some files are lost or damaged. In this case, check whether :ref:`8.d <mrs_01_1664__en-us_topic_0000001219350541_l63f4856203e9425f9a23113c3d13f665>` is correct and run the **hdfs fsck** *Name of the damaged file* **-delete** command.

**Changing the storage directory of a single DataNode instance**

12. .. _mrs_01_1664__en-us_topic_0000001219350541_lab34cabb4d324166acebeb18e1098884:

    Choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **Instance**. Select the HDFS instance whose storage directory needs to be modified, and choose **More** > **Stop Instance**.

13. Log in to the DataNode node as user **root**, and perform the following operations:

    a. Create a target directory.

       For example, to create a target directory **${BIGDATA_DATA_HOME}/hadoop/data3/dn**, run the following commands:

       **mkdir** **${BIGDATA_DATA_HOME}/hadoop/data3** and **mkdir ${BIGDATA_DATA_HOME}/hadoop/data3/dn**

    b. Mount the target directory to the new disk.

       For example, mount **${BIGDATA_DATA_HOME}/hadoop/data3** to the new disk.

    c. Modify permissions on the new directory.

       For example, to create a target directory **${BIGDATA_DATA_HOME}/hadoop/data3/dn**, run the following commands:

       **chmod 700** **${BIGDATA_DATA_HOME}/hadoop/data3/dn -R** and **chown omm:wheel** **${BIGDATA_DATA_HOME}/hadoop/data3/dn -R**

    d. Copy the data to the target directory.

       For example, if the old directory is **${BIGDATA_DATA_HOME}/hadoop/data1/dn** and the target directory is **${BIGDATA_DATA_HOME}/hadoop/data3/dn**, run the following command:

       **cp -af** **${BIGDATA_DATA_HOME}/hadoop/data1/dn/\*** **${BIGDATA_DATA_HOME}/hadoop/data3/dn**

14. On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Service** > **HDFS** > **Instance**. Click the specified DataNode instance and go to the **Configurations** page.

    Change the value of **dfs.datanode.data.dir** from the default value **%{@auto.detect.datapart.dn}** to the new target directory, for example, **${BIGDATA_DATA_HOME}/hadoop/data3/dn**.

    For example, the original data storage directories are **/srv/BigData/hadoop/data1,/srv/BigData/hadoop/data2**. To migrate data from the **/srv/BigData/hadoop/data1** directory to the newly created **/srv/BigData/hadoop/data3** directory, replace the whole parameter with **/srv/BigData/hadoop/data2,/srv/BigData/hadoop/data3**.

15. Click **Save**, and then click **OK**.

    **Operation succeeded** is displayed. click **Finish**.

16. Choose **More** > **Restart Instance** to restart the DataNode instance.
