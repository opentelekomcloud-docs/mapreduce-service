:original_name: mrs_01_1667.html

.. _mrs_01_1667:

Balancing DataNode Capacity
===========================

Scenario
--------

In the HDFS cluster, unbalanced disk usage among DataNodes may occur, for example, when new DataNodes are added to the cluster. Unbalanced disk usage may result in multiple problems. For example, MapReduce applications cannot make full use of local computing advantages, network bandwidth usage between data nodes cannot be optimal, or node disks cannot be used. Therefore, the system administrator needs to periodically check and maintain DataNode data balance.

HDFS provides a capacity balancing program Balancer. By running Balancer, you can balance the HDFS cluster and ensure that the difference between the disk usage of each DataNode and that of the HDFS cluster does not exceed the threshold. DataNode disk usage before and after balancing is shown in :ref:`Figure 1 <mrs_01_1667__en-us_topic_0000001219231321_ff269b77c9222460985503fffcebf980e>` and :ref:`Figure 2 <mrs_01_1667__en-us_topic_0000001219231321_fee19cefb9d104f238448abdcf62f1e49>`, respectively.

.. _mrs_01_1667__en-us_topic_0000001219231321_ff269b77c9222460985503fffcebf980e:

.. figure:: /_static/images/en-us_image_0000001295899880.png
   :alt: **Figure 1** DataNode disk usage before balancing

   **Figure 1** DataNode disk usage before balancing

.. _mrs_01_1667__en-us_topic_0000001219231321_fee19cefb9d104f238448abdcf62f1e49:

.. figure:: /_static/images/en-us_image_0000001295739916.png
   :alt: **Figure 2** DataNode disk usage after balancing

   **Figure 2** DataNode disk usage after balancing

The time of the balancing operation is affected by the following two factors:

#. Total amount of data to be migrated:

   The data volume of each DataNode must be greater than (Average usage - Threshold) x Average data volume and less than (Average usage + Threshold) x Average data volume. If the actual data volume is less than the minimum value or greater than the maximum value, imbalance occurs. The system sets the largest deviation volume on all DataNodes as the total data volume to be migrated.

#. Balancer migration is performed in sequence in iteration mode. The amount of data to be migrated in each iteration does not exceed 10 GB, and the usage of each iteration is recalculated.

Therefore, for a cluster, you can estimate the time consumed by each iteration (by observing the time consumed by each iteration recorded in balancer logs) and divide the total data volume by 10 GB to estimate the task execution time.

The balancer can be started or stopped at any time.

Impact on the System
--------------------

-  The balance operation occupies network bandwidth resources of DataNodes. Perform the operation during maintenance based on service requirements.
-  The balance operation may affect the running services if the bandwidth traffic (the default bandwidth control is 20 MB/s) is reset or the data volume is increased.

Prerequisites
-------------

The client has been installed.

Procedure
---------

#. Log in to the node where the client is installed as a client installation user. Run the following command to switch to the client installation directory, for example, **/opt/client**:

   **cd /opt/client**

   .. note::

      If the cluster is in normal mode, run the **su - omm** command to switch to user **omm**.

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, run the following command to authenticate the HDFS identity:

   **kinit hdfs**

#. Determine whether to adjust the bandwidth control.

   -  If yes, go to :ref:`5 <mrs_01_1667__en-us_topic_0000001219231321_l91d088e58d8d4bbbb720317d843ca5d3>`.
   -  If no, go to :ref:`6 <mrs_01_1667__en-us_topic_0000001219231321_ld8ed77b8b7c745308eea6a68de2f4233>`.

#. .. _mrs_01_1667__en-us_topic_0000001219231321_l91d088e58d8d4bbbb720317d843ca5d3:

   Run the following command to change the maximum bandwidth of Balancer, and then go to :ref:`6 <mrs_01_1667__en-us_topic_0000001219231321_ld8ed77b8b7c745308eea6a68de2f4233>`.

   **hdfs dfsadmin -setBalancerBandwidth <bandwidth in bytes per second>**

   *<bandwidth in bytes per second>* indicates the bandwidth control value, in bytes. For example, to set the bandwidth control to 20 MB/s (the corresponding value is 20971520), run the following command:

   **hdfs dfsadmin -setBalancerBandwidth** **20971520**

   .. note::

      -  The default bandwidth control is 20 MB/s. This value is applicable to the scenario where the current cluster uses the 10GE network and services are being executed. If the service idle time window is insufficient for balance maintenance, you can increase the value of this parameter to shorten the balance time, for example, to 209715200 (200 MB/s).
      -  The value of this parameter depends on the networking. If the cluster load is high, you can change the value to 209715200 (200 MB/s). If the cluster is idle, you can change the value to 1073741824 (1 GB/s).
      -  If the bandwidth of the DataNodes cannot reach the specified maximum bandwidth, modify the HDFS parameter **dfs.datanode.balance.max.concurrent.moves** on FusionInsight Manager, and change the number of threads for balancing on each DataNode to **32** and restart the HDFS service.

#. .. _mrs_01_1667__en-us_topic_0000001219231321_ld8ed77b8b7c745308eea6a68de2f4233:

   Run the following command to start the balance task:

   **bash /opt/client/HDFS/hadoop/sbin/start-balancer.sh -threshold <threshold of balancer\ >**

   **-threshold** specifies the deviation value of the DataNode disk usage, which is used for determining whether the HDFS data is balanced. When the difference between the disk usage of each DataNode and the average disk usage of the entire HDFS cluster is less than this threshold, the system considers that the HDFS cluster has been balanced and ends the balance task.

   For example, to set deviation rate to 5%, run the following command:

   **bash /opt/client/HDFS/hadoop/sbin/start-balancer.sh -threshold 5**

   .. note::

      -  The preceding command executes the task in the background. You can query related logs in the **hadoop-root-balancer-**\ *host name*\ **.out log** file in the **/opt/client/HDFS/hadoop/logs** directory of the host.

      -  To stop the balance task, run the following command:

         **bash /opt/client/HDFS/hadoop/sbin/stop-balancer.sh**

      -  If only data on some nodes needs to be balanced, you can add the **-include** parameter in the script to specify the nodes to be migrated. You can run commands to view the usage of different parameters.

      -  **/opt/client** is the client installation directory. If the directory is inconsistent, replace it.

      -  If the command fails to be executed and the error information **Failed to APPEND_FILE /system/balancer.id** is displayed in the log, run the following command to forcibly delete **/system/balancer.id** and run the **start-balancer.sh** script again:

         **hdfs dfs -rm -f /system/balancer.id**

#. If the following information is displayed, the balancing is complete and the system automatically exits the task:

   .. code-block::

      Apr 01, 2016 01:01:01 PM  Balancing took 23.3333 minutes

   After you run the script in :ref:`6 <mrs_01_1667__en-us_topic_0000001219231321_ld8ed77b8b7c745308eea6a68de2f4233>`, the **hadoop-root-balancer-**\ *Host name*\ **.out log** file is generated in the client installation directory **/opt/client/HDFS/hadoop/logs**. You can view the following information in the log:

   -  Time Stamp
   -  Bytes Already Moved
   -  Bytes Left To Move
   -  Bytes Being Moved

Related Tasks
-------------

**Enable automatic execution of the balance task**

#. Log in to FusionInsight Manager.

#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **Configurations**, select **All Configurations**, search for the following parameters, and change the parameter values.

   -  **dfs.balancer.auto.enable** indicates whether to enable automatic balance task execution. The default value **false** indicates that automatic balance task execution is disabled. The value **true** indicates that automatic execution is enabled.

   -  **dfs.balancer.auto.cron.expression** indicates the task execution time. The default value **0 1 \* \* 6** indicates that the task is executed at 01:00 every Saturday. This parameter is valid only when the automatic execution is enabled.

      :ref:`Table 1 <mrs_01_1667__en-us_topic_0000001219231321_t3d64fdb3254a42beaed3c5e4c7087501>` describes the expression for modifying this parameter. **\*** indicates consecutive time segments.

      .. _mrs_01_1667__en-us_topic_0000001219231321_t3d64fdb3254a42beaed3c5e4c7087501:

      .. table:: **Table 1** Parameters in the execution expression

         ====== ===========================================================
         Column Description
         ====== ===========================================================
         1      Minute. The value ranges from 0 to 59.
         2      Hour. The value ranges from 0 to 23.
         3      Date. The value ranges from 1 to 31.
         4      Month. The value ranges from 1 to 12.
         5      Week. The value ranges from 0 to 6. **0** indicates Sunday.
         ====== ===========================================================

   -  **dfs.balancer.auto.stop.cron.expression** indicates the task ending time. The default value is empty, indicating that the running balance task is not automatically stopped. For example, **0 5 \* \* 6** indicates that the balance task is stopped at 05:00 every Saturday. This parameter is valid only when the automatic execution is enabled.

      :ref:`Table 1 <mrs_01_1667__en-us_topic_0000001219231321_t3d64fdb3254a42beaed3c5e4c7087501>` describes the expression for modifying this parameter. **\*** indicates consecutive time segments.

#. Running parameters of the balance task that is automatically executed are shown in :ref:`Table 2 <mrs_01_1667__en-us_topic_0000001219231321_tc3bff391b0c14479916d9097f5e28238>`.

   .. _mrs_01_1667__en-us_topic_0000001219231321_tc3bff391b0c14479916d9097f5e28238:

   .. table:: **Table 2** Running parameters of the automatic balancer

      +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
      | Parameter                           | Parameter description                                                                                                                                                                                                                                                                                                                                                     | Default Value                       |
      +=====================================+===========================================================================================================================================================================================================================================================================================================================================================================+=====================================+
      | dfs.balancer.auto.threshold         | Specifies the balancing threshold of the disk capacity percentage. This parameter is valid only when **dfs.balancer.auto.enable** is set to **true**.                                                                                                                                                                                                                     | 10                                  |
      +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
      | dfs.balancer.auto.exclude.datanodes | Specifies the list of DataNodes on which automatic disk balancing is not required. This parameter is valid only when **dfs.balancer.auto.enable** is set to **true**.                                                                                                                                                                                                     | The value is left blank by default. |
      +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
      | dfs.balancer.auto.bandwidthPerSec   | Specifies the maximum bandwidth (MB/s) of each DataNode for load balancing.                                                                                                                                                                                                                                                                                               | 20                                  |
      +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
      | dfs.balancer.auto.maxIdleIterations | Specifies the maximum number of consecutive idle iterations of Balancer. An idle iteration is an iteration without moving blocks. When the number of consecutive idle iterations reaches the maximum number, the balance task ends. The value **-1** indicates infinity.                                                                                                  | 5                                   |
      +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+
      | dfs.balancer.auto.maxDataNodesNum   | Controls the number of DataNodes that perform automatic balance tasks. Assume that the value of this parameter is *N*. If *N* is greater than 0, data is balanced between *N* DataNodes with the highest percentage of remaining space and *N* DataNodes with the lowest percentage of remaining space. If *N* is 0, data is balanced among all DataNodes in the cluster. | 5                                   |
      +-------------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------+

#. Click **Save** to make configurations take effect. You do not need to restart the HDFS service.

   Go to the **/var/log/Bigdata/hdfs/nn/hadoop-omm-balancer-**\ *Host name*\ **.log** file to view the task execution logs saved in the active NameNode.
