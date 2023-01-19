:original_name: mrs_01_2096.html

.. _mrs_01_2096:

Changing the ZooKeeper Storage Directory
========================================

Scenario
--------

When the defined storage directory of ZooKeeper is incorrect, or when the storage plan of ZooKeeper is changed, log in to FusionInsight Manager to change the storage directory of ZooKeeper to ensure ZooKeeper runs properly. The storage directory of ZooKeeper includes the local data storage directory **dataDir**. Changing the ZooKeeper storage directory includes the following scenarios:

-  Change the storage directory of the ZooKeeper role. In this way, the storage directories of all the ZooKeeper instances are also changed.
-  Change the storage directory of a single ZooKeeper instance. In this way, only the storage directory of this ZooKeeper instance is changed, and the storage directories of other ZooKeeper instances are not changed.

Impact on the System
--------------------

-  ZooKeeper and associated services needs to be stopped and restarted during the process of changing the storage directory of ZooKeeper, and the cluster cannot provide services before restarted.
-  The ZooKeeper instance needs to stopped and restarted during the process of changing the storage directory of the instance, and the ZooKeeper instance at this node cannot provide services before restarted.

Prerequisites
-------------

-  New disks have been prepared and installed on each data node, and the disks are formatted.
-  New directories have been planned for storing data in the original directories.
-  The system administrator account **admin** has been prepared.

Procedure
---------

**Check the environment.**

#. Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** to check whether **Running Status** of ZooKeeper is **Normal**.

   -  If yes, go to :ref:`3 <mrs_01_2096__en-us_topic_0000001173949506_lea936dc5deb6448ea00cd21461dc3094>`.
   -  If no, the ZooKeeper status is unhealthy. Go to :ref:`2 <mrs_01_2096__en-us_topic_0000001173949506_lcdb1dc70dbb84667b8f174b2567f000b>`.

#. .. _mrs_01_2096__en-us_topic_0000001173949506_lcdb1dc70dbb84667b8f174b2567f000b:

   Rectify the ZooKeeper fault.

#. .. _mrs_01_2096__en-us_topic_0000001173949506_lea936dc5deb6448ea00cd21461dc3094:

   Determine whether to change the storage directory of the ZooKeeper role or that of a ZooKeeper instance:

   -  To change the storage directory of the ZooKeeper role, go to :ref:`4 <mrs_01_2096__en-us_topic_0000001173949506_li3363814122716>`.
   -  To change the storage directory of a single ZooKeeper instance, go to :ref:`9 <mrs_01_2096__en-us_topic_0000001173949506_li51171617171416>`.

**Change the storage directory of the ZooKeeper role.**

4. .. _mrs_01_2096__en-us_topic_0000001173949506_li3363814122716:

   Choose **Cluster** > *Name of the desired cluster* > **Services** > **ZooKeeper** > **Stop** to stop the ZooKeeper service.

5. Log in to each node where the ZooKeeper service is installed as user **root** and perform the following operations:

   a. Create a target directory.

      For example, to create the target directory **${BIGDATA_DATA_HOME}/zookeeper2**, run the following command:

      **mkdir ${BIGDATA_DATA_HOME}/zookeeper2**.

   b. Format the new disk, and mount the target directory to the new disk. For example, mount **${BIGDATA_DATA_HOME}/zookeeper2** to the new disk.

   c. Modify permissions on the new directory.

      For example, the new directory is **${BIGDATA_DATA_HOME}/zookeeper2**.

      Run **chmod 700 ${BIGDATA_DATA_HOME}/zookeeper2** and **chown omm:wheel ${BIGDATA_DATA_HOME}/zookeeper2**.

   d. Run the following commands to copy the original data to the new directory:

      For example, run **cp -pr ${BIGDATA_DATA_HOME}/zookeeper/version-2/ ${BIGDATA_DATA_HOME}/zookeeper2/**

      **cp -pr ${BIGDATA_DATA_HOME}/zookeeper/myid ${BIGDATA_DATA_HOME}/zookeeper2/**

6. On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Service** > **ZooKeeper** > **Configuration** to go to the configuration page of the ZooKeeper service.

   Set **dataDir** of ZooKeeper and quorumpeer to the new target directory, such as **${BIGDATA_DATA_HOME}/zookeeper2**.

7. Click **Save**, and then click **OK**. Restart the ZooKeeper service.

   Click **Finish** when the system displays "Operation successful". ZooKeeper is successfully started.

8. Rename the original storage directory **${BIGDATA_DATA_HOME}/zookeeper**. If the directory is a root directory that is mounted to an independent disk, remove the disk before renaming the directory and no further action is required.

**Change the storage directory of a single ZooKeeper instance.**

9.  .. _mrs_01_2096__en-us_topic_0000001173949506_li51171617171416:

    Choose **Cluster** > *Name of the desired cluster* > **Service** > **ZooKeeper** > **Instances**. Select the ZooKeeper instance whose storage directory needs to be modified, and choose **More** > **Stop Instance**.

10. Log in to the ZooKeeper node as user **root**, and perform the following operations:

    a. Create a target directory.

       For example, to create the target directory **${BIGDATA_DATA_HOME}/zookeeper2**, run the following command:

       **mkdir ${BIGDATA_DATA_HOME}/zookeeper2**.

    b. Mount the target directory to the new disk. For example, mount **${BIGDATA_DATA_HOME}/yarn/data2** to the new disk.

    c. Modify permissions on the new directory.

       For example, to modify permissions on the **${BIGDATA_DATA_HOME}/yarn/data2** directory, run the following commands:

       **chmod 700 ${BIGDATA_DATA_HOME}/zookeeper2** and **chown omm:wheel ${BIGDATA_DATA_HOME}/zookeeper2**

    d. Run the following commands to copy the original data to the new directory:

       For example, run **cp -pr ${BIGDATA_DATA_HOME}/zookeeper/version-2/ ${BIGDATA_DATA_HOME}/zookeeper2/**

       **cp -pr ${BIGDATA_DATA_HOME}/zookeeper/myid ${BIGDATA_DATA_HOME}/zookeeper2/**

11. On FusionInsight Manager, click the specified ZooKeeper instance, and switch to the **Instance Configuration** page.

    Set **dataDir** of ZooKeeper and quorumpeer to the new target directory, such as **${BIGDATA_DATA_HOME}/zookeeper2**.

12. Click **Save**, and then click **OK**. Restart the ZooKeeper instance.

    Click **Finish** when the system displays "Operation successful". The ZooKeeper instance is successfully started.

13. Rename the original storage directory **${BIGDATA_DATA_HOME}/zookeeper**. If the directory is a root directory that is mounted to an independent disk, remove the disk before renaming the directory and no further action is required.
