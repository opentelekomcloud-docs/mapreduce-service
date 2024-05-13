:original_name: admin_guide_000040.html

.. _admin_guide_000040:

Decommissioning and Recommissioning an Instance
===============================================

Scenario
--------

Some role instances provide services for external services in distributed and parallel mode. Services independently store information about whether each instance can be used. Therefore, you need to use MRS Manager to recommission or decommission these instances to change the instance running status.

Some instances do not support the recommissioning and decommissioning functions.

.. note::

   The following roles support decommissioning and recommissioning: HDFS DataNode, YARN NodeManager, and HBase RegionServer.

   -  If the number of the DataNodes is less than or equal to that of HDFS replicas, decommissioning cannot be performed. If the number of HDFS replicas is three and the number of DataNodes is less than four in the system, decommissioning cannot be performed. In this case, an error will be reported and force MRS Manager to exit the decommissioning 30 minutes after MRS Manager attempts to perform the decommissioning.
   -  During MapReduce task execution, files with 10 replicas are generated. Therefore, if the number of DataNode instances is less than 10, decommissioning cannot be performed.
   -  If the number of DataNode racks (the number of racks is determined by the number of racks configured for each DataNode) is greater than 1 before the decommissioning, and after some DataNodes are decommissioned, that of the remaining DataNodes changes to 1, the decommissioning will fail. Therefore, before decommissioning DataNode instances, you need to evaluate the impact of decommissioning on the number of racks to adjust the DataNodes to be decommissioned.
   -  If multiple DataNodes are decommissioned at the same time, and each of them stores a large volume of data, the DataNodes may fail to be decommissioned due to timeout. To avoid this problem, it is recommended that one DataNode be decommissioned each time and multiple decommissioning operations be performed.

Procedure
---------

#. Perform the following steps to perform a health check for the DataNodes before decommissioning:

   a. Log in to the client installation node as a client user and switch to the client installation directory.

   b. For a security cluster, use user **hdfs** for permission authentication.

      .. code-block::

         source bigdata_env               #Configure client environment variables.
         kinit hdfs                       #Configure kinit authentication.
         Password for hdfs@HADOOP.COM:    #Enter the login password of user hdfs.

   c. Run the **hdfs fsck / -list-corruptfileblocks** command, and check the returned result.

      -  If "has 0 CORRUPT files" is displayed, go to :ref:`2 <admin_guide_000040__en-us_topic_0046737055_step_2>`.
      -  If the result does not contain "has 0 CORRUPT files" and the name of the damaged file is returned, go to :ref:`1.d <admin_guide_000040__en-us_topic_0046737055_step_1e>`.

   d. .. _admin_guide_000040__en-us_topic_0046737055_step_1e:

      Run the **hdfs dfs -rm** *Name of the damaged file* command to delete the damaged file.

      .. note::

         Deleting a file or folder is a high-risk operation. Ensure that the file or folder is no longer required before performing this operation.

#. .. _admin_guide_000040__en-us_topic_0046737055_step_2:

   Log in to MRS Manager.

#. Choose **Cluster** > *Name of the desired cluster* > **Services**.

#. Click the specified service name on the service management page. On the displayed page, click the **Instance** tab.

#. Select the specified role instance to be decommissioned.

#. Select **Decommission** or **Recommission** from the **More** drop-down list.

   In the displayed dialog box, enter the password of the current login user and click **OK**.

   Select **I confirm to decommission these instances and accept the consequence of service performance deterioration** and click **OK** to perform the corresponding operation.

   .. note::

      During the instance decommissioning, if the service corresponding to the instance is restarted in the cluster using another browser, MRS Manager displays a message indicating that the instance decommissioning is stopped, but the operating status of the instance is displayed as **Started**. In this case, the instance has been decommissioned on the background. You need to decommission the instance again to synchronize the operating status.
