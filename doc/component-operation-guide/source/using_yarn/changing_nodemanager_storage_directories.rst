:original_name: mrs_01_0856.html

.. _mrs_01_0856:

Changing NodeManager Storage Directories
========================================

Scenario
--------

If the storage directories defined by the Yarn NodeManager are incorrect or the Yarn storage plan changes, the system administrator needs to modify the NodeManager storage directories on Manager to ensure that the Yarn works properly. The storage directories of NodeManager include the local storage directory **yarn.nodemanager.local-dirs** and log directory **yarn.nodemanager.log-dirs**. Changing the ZooKeeper storage directory includes the following scenarios:

-  Change the storage directory of the NodeManager role. In this way, the storage directories of all NodeManager instances are changed.
-  Change the storage directory of a single NodeManager instance. In this way, only the storage directory of this instance is changed, and the storage directories of other instances remain the same.

Impact on the System
--------------------

-  The cluster needs to stopped and restarted during the process of changing the storage directory of the NodeManager role, and the cluster cannot provide services before started.
-  The NodeManager instance needs to stopped and restarted during the process of changing the storage directory of the instance, and the instance at this node cannot provide services before it is started.
-  The directory for storing service parameter configurations must also be updated.
-  After the storage directories of NodeManager are changed, you need to download and install the client again.

Prerequisites
-------------

-  New disks have been prepared and installed on each data node, and the disks are formatted.
-  New directories have been planned for storing data in the original directories.
-  The system administrator account **admin** has been prepared.

Procedure
---------

For versions earlier than MRS 1.9.2, perform the following operations:

#. Check the environment.

   a. Log in to MRS Manager and click the cluster name. Choose **Services** and check whether health status of Yarn is **Good**.

      -  If yes, go to :ref:`1.c <mrs_01_0856__li64045734911>`.
      -  If no, go to :ref:`1.b <mrs_01_0856__li174035711490>`.

   b. .. _mrs_01_0856__li174035711490:

      Rectify the Yarn fault. No further action is required.

   c. .. _mrs_01_0856__li64045734911:

      Determine whether to change the storage directory of the NodeManager role or that of a single NodeManager instance:

      -  To change the storage directory of the NodeManager role, go to :ref:`2 <mrs_01_0856__li104015571499>`.
      -  To change the storage directory of a single NodeManager instance, go to :ref:`3 <mrs_01_0856__li1041165717494>`.

#. .. _mrs_01_0856__li104015571499:

   Change the storage directory of the NodeManager role.

   a. Click the cluster name and choose **Services** > **Yarn** > **Stop** to stop the Yarn service.

   b. Log in as user **root** to each node on which the Yarn service is installed, and perform the following operations:

      #. Create a target directory.

         For example, to create the target directory **${BIGDATA_DATA_HOME}/data2**, run the following command:

         **mkdir ${BIGDATA_DATA_HOME}/data2**

      #. Mount the target directory to the new disk.

         For example, mount **${BIGDATA_DATA_HOME}/data2** to the new disk.

      #. Modify permissions on the new directory.

         For example, to modify permissions on the **${BIGDATA_DATA_HOME}/data2** directory, run the following commands:

         **chmod 750 ${BIGDATA_DATA_HOME}/data2 -R** and **chown omm:wheel ${BIGDATA_DATA_HOME}/data2 -R**

   c. On MRS Manager, click the cluster name. Choose **Services** > **Yarn** > **Instance**. Select the NodeManager instance of the corresponding host. Choose **Instance Configuration** > **All Configurations**.

      Change the value of **yarn.nodemanager.local-dirs** or **yarn.nodemanager.log-dirs** to the new target directory.

      For example, change the value of **yarn.nodemanager.local-dirs** or **yarn.nodemanager.log-dirs** to **/srv/BigData/data2/nm/containerlogs**.

   d. Click **Save Configuration**, select **Restart the affected services or instances**, and click **OK** Restart the Yarn service.

      Click **Finish** when the system displays "Operation successful". Yarn is successfully started. No further action is required.

#. .. _mrs_01_0856__li1041165717494:

   Change the storage directory of a single NodeManager instance.

   a. Click the cluster name. Choose **Services** > **Yarn** > **Instance**. Select the NodeManager instance whose storage directory needs to be modified, and choose **More** > **Stop Instance**.

   b. Log in to the NodeManager node as user **root** and perform the following operations:

      #. Create a target directory.

         For example, to create the target directory **${BIGDATA_DATA_HOME}/data2**, run the following command:

         **mkdir ${BIGDATA_DATA_HOME}/data2**

      #. Mount the target directory to the new disk.

         For example, mount **${BIGDATA_DATA_HOME}/data2** to the new disk.

      #. Modify permissions on the new directory.

         For example, to modify permissions on the **${BIGDATA_DATA_HOME}/data2** directory, run the following commands:

         **chmod 750 ${BIGDATA_DATA_HOME}/data2 -R** and **chown omm:wheel ${BIGDATA_DATA_HOME}/data2 -R**

   c. On MRS Manager, click the specified NodeManager instance and switch to the **Instance Configuration** tab page.

      Change the value of **yarn.nodemanager.local-dirs** or **yarn.nodemanager.log-dirs** to the new target directory.

      For example, change the value of **yarn.nodemanager.local-dirs** or **yarn.nodemanager.log-dirs** to **/srv/BigData/data2/nm/containerlogs**.

   d. Click **Save Configuration** and select **Restart the affected services or instances**. Click **OK** to restart the NodeManager instance.

      Click **Finish** when the system displays "Operation successful". The NodeManager instance is successfully started.

For versions earlier than MRS 3.\ *x*, perform the following operations:

#. Check the environment.

   a. Log in to the MRS console. In the left navigation pane, choose **Clusters** > **Active Clusters**, and click a cluster name. Choose **Components** and check whether health status of Yarn is **Good**.

      -  If yes, go to :ref:`1.c <mrs_01_0856__la5078ba0645147aba6b90f071779368f>`.
      -  If no, the Yarn status is unhealthy. Go to :ref:`1.b <mrs_01_0856__le3afaf4553c243db9a4849977eadb16f>`.

   b. .. _mrs_01_0856__le3afaf4553c243db9a4849977eadb16f:

      Rectify the Yarn fault. No further action is required.

   c. .. _mrs_01_0856__la5078ba0645147aba6b90f071779368f:

      Determine whether to change the storage directory of the NodeManager role or that of a single NodeManager instance:

      -  To change the storage directory of the NodeManager role, go to :ref:`2 <mrs_01_0856__le6194cc33c3d4e1f8c058a988180165c>`.
      -  To change the storage directory of a single NodeManager instance, go to :ref:`3 <mrs_01_0856__l74bdf880464b4eb18f01531e8355e3c4>`.

#. .. _mrs_01_0856__le6194cc33c3d4e1f8c058a988180165c:

   Change the storage directory of the NodeManager role.

   a. Choose **Clusters** > **Active Clusters**, and click a cluster name. Choose **Components** > **Yarn** > **Stop** to stop the Yarn service.

   b. Log in to the ECS server and go to each node where Yarn is installed as user **root**. Perform the following operations:

      #. Create a target directory.

         For example, to create the target directory **${BIGDATA_DATA_HOME}/data2**, run the following command:

         **mkdir ${BIGDATA_DATA_HOME}/data2**

      #. Mount the target directory to the new disk.

         For example, mount **${BIGDATA_DATA_HOME}/data2** to the new disk.

      #. Modify permissions on the new directory.

         For example, to modify permissions on the **${BIGDATA_DATA_HOME}/data2** directory, run the following commands:

         **chmod 750 ${BIGDATA_DATA_HOME}/data2 -R** and **chown omm:wheel ${BIGDATA_DATA_HOME}/data2 -R**

   c. On the MRS console, choose **Clusters** > **Active Clusters** and click a cluster name. Choose **Components** > **Yarn** > **Instances**. Select the NodeManager instance of the corresponding host. Choose **Instance Configuration** > **All Configurations**.

      Change the value of **yarn.nodemanager.local-dirs** or **yarn.nodemanager.log-dirs** to the new target directory.

      For example, change the value of **yarn.nodemanager.local-dirs** or **yarn.nodemanager.log-dirs** to **/srv/BigData/data2/nm/containerlogs**.

   d. Click **Save Configuration**, select **Restart the affected services or instances**, and click **OK** Restart the Yarn service.

      Click **Finish** when the system displays "Operation successful". Yarn is successfully started. No further action is required.

#. .. _mrs_01_0856__l74bdf880464b4eb18f01531e8355e3c4:

   Change the storage directory of a single NodeManager instance.

   a. Choose **Clusters** > **Active Clusters**, and click a cluster name. Choose **Components** > **Yarn** > **Instances**. Select the NodeManager instance whose storage directory needs to be modified, and choose **More** > **Stop Instance**.

   b. Log in to the ECS and go to the NodeManager node as user **root**. Perform the following operations:

      #. Create a target directory.

         For example, to create the target directory **${BIGDATA_DATA_HOME}/data2**, run the following command:

         **mkdir ${BIGDATA_DATA_HOME}/data2**

      #. Mount the target directory to the new disk.

         For example, mount **${BIGDATA_DATA_HOME}/data2** to the new disk.

      #. Modify permissions on the new directory.

         For example, to modify permissions on the **${BIGDATA_DATA_HOME}/data2** directory, run the following commands:

         **chmod 750 ${BIGDATA_DATA_HOME}/data2 -R** and **chown omm:wheel ${BIGDATA_DATA_HOME}/data2 -R**

   c. On the MRS console, click the specified NodeManager instance and switch to the **Instance Configuration** tab page.

      Change the value of **yarn.nodemanager.local-dirs** or **yarn.nodemanager.log-dirs** to the new target directory.

      For example, change the value of **yarn.nodemanager.local-dirs** or **yarn.nodemanager.log-dirs** to **/srv/BigData/data2/nm/containerlogs**.

   d. Click **Save Configuration** and select **Restart the affected services or instances**. Click **OK** to restart the NodeManager instance.

      Click **Finish** when the system displays "Operation successful". The NodeManager instance is successfully started.

For MRS 3.\ *x* or later, perform the following operations:

#. Check the environment.

   a. Log in to Manager, choose **Cluster** > *Name of the desired cluster* > **Service** to check whether **Running Status** of Yarn is **Normal**.

      -  If yes, go to :ref:`1.c <mrs_01_0856__li988561895113>`.
      -  If no, the Yarn status is unhealthy. In this case, go to :ref:`1.b <mrs_01_0856__li18885518135118>`.

   b. .. _mrs_01_0856__li18885518135118:

      Rectify faults of Yarn. No further action is required.

   c. .. _mrs_01_0856__li988561895113:

      Determine whether to change the storage directory of the NodeManager role or that of a single NodeManager instance:

      -  To change the storage directory of the NodeManager role, go to :ref:`2 <mrs_01_0856__li2885101825117>`.
      -  To change the storage directory of a single NodeManager instance, go to :ref:`3 <mrs_01_0856__li1288531845117>`.

#. .. _mrs_01_0856__li2885101825117:

   Change the storage directory of the NodeManager role.

   a. Choose **Cluster** > *Name of the desired cluster* > **Service** > **Yarn** > **Stop** to stop the Yarn service.

   b. Log in to each data node where the Yarn service is installed as user **root** and perform the following operations:

      #. Create a target directory.

         For example, to create the target directory **${BIGDATA_DATA_HOME}/data2**, run the following command:

         **mkdir ${BIGDATA_DATA_HOME}/data2**

      #. Mount the target directory to the new disk.

         For example, mount **${BIGDATA_DATA_HOME}/data2** to the new disk.

      #. Modify permissions on the new directory.

         For example, to modify permissions on the **${BIGDATA_DATA_HOME}/data2** directory, run the following commands:

         **chmod 750 ${BIGDATA_DATA_HOME}/data2 -R** and **chown omm:wheel ${BIGDATA_DATA_HOME}/data2 -R**

   c. On the Manager portal, choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn** > **Instance**. Select the NodeManager instance of the corresponding host, click **Instance Configuration**, and select \ **All Configurations**.

      Change the value of **yarn.nodemanager.local-dirs** or **yarn.nodemanager.log-dirs** to the new target directory.

      For example, change the value of **yarn.nodemanager.local-dirs** or **yarn.nodemanager.log-dirs** to **/srv/BigData/data2/nm/containerlogs**.

   d. Click **Save**, and then click **OK**. Restart the Yarn service.

      Click **Finish** when the system displays "Operation successful". Yarn is successfully started. No further action is required.

#. .. _mrs_01_0856__li1288531845117:

   Change the storage directory of a single NodeManager instance.

   a. Choose **Cluster** > *Name of the desired cluster* > **Service** > **Yarn** > **Instance**, select the NodeManager instance whose storage directory needs to be modified, and choose **More** > **Stop**.

   b. Log in to the NodeManager node as user **root**, and perform the following operations:

      #. Create a target directory.

         For example, to create the target directory **${BIGDATA_DATA_HOME}/data2**, run the following command:

         **mkdir ${BIGDATA_DATA_HOME}/data2**

      #. Mount the target directory to the new disk.

         For example, mount **${BIGDATA_DATA_HOME}/data2** to the new disk.

      #. Modify permissions on the new directory.

         For example, to modify permissions on the **${BIGDATA_DATA_HOME}/data2** directory, run the following commands:

         **chmod 750 ${BIGDATA_DATA_HOME}/data2 -R** and **chown omm:wheel ${BIGDATA_DATA_HOME}/data2 -R**

   c. On Manager, click the specified NodeManager instance, and switch to the **Instance Configuration** page.

      Change the value of **yarn.nodemanager.local-dirs** or **yarn.nodemanager.log-dirs** to the new target directory.

      For example, change the value of **yarn.nodemanager.local-dirs** or **yarn.nodemanager.log-dirs** to **/srv/BigData/data2/nm/containerlogs**.

   d. Click **Save**, and then click **OK** to restart the NodeManager instance.

      Click **Finish** when the system displays "Operation successful". The NodeManager instance is successfully started.
