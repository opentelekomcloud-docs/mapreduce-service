:original_name: en-us_topic_0012799688.html

.. _en-us_topic_0012799688:

Cluster List
============

You can quickly view the status of all clusters and jobs by viewing the dashboard information, and obtain relevant MRS documents from **Overview** in the left navigation pane on the MRS console.

MRS is used to manage and analyze massive data. It is easy to use. You can create a cluster and add MapReduce, Spark, and Hive jobs to the cluster to analyze and process user data. After being processed, you can transmit the data in SSL encryption mode to OBS to ensure data integrity and confidentiality.

Cluster Status
--------------

:ref:`Table 1 <en-us_topic_0012799688__table164091551415>` lists the statuses of all MRS clusters after you log in to the MRS management console.

.. _en-us_topic_0012799688__table164091551415:

.. table:: **Table 1** Cluster status

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Status                            | Description                                                                                                                                                                                                     |
   +===================================+=================================================================================================================================================================================================================+
   | Starting                          | If a cluster is being created, the cluster is in the **Starting** state.                                                                                                                                        |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Running                           | If a cluster is created successfully and all components in the cluster are normal, the cluster is in the **Running** state.                                                                                     |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Scaling out                       | If the Core or Task node in a cluster is being added, the cluster is in the **Scaling out** state.                                                                                                              |
   |                                   |                                                                                                                                                                                                                 |
   |                                   | .. note::                                                                                                                                                                                                       |
   |                                   |                                                                                                                                                                                                                 |
   |                                   |    If the cluster scale-out fails, you can add node to the cluster again.                                                                                                                                       |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Scaling in                        | If you stop, delete, change or reinstall the OSs of cluster nodes, and modify the specifications of the cluster node, the cluster nodes are being terminated. Then, the cluster is in the **Scaling in** state. |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Abnormal                          | If some components in a cluster are abnormal, the cluster is **Abnormal**.                                                                                                                                      |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Terminating                       | If a cluster node is being terminated, the cluster is in the **Terminating** state.                                                                                                                             |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Terminated                        | The cluster has been terminated. This parameter is displayed only in **Cluster History**.                                                                                                                       |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Scaling up Master node            | If the specifications of a master node are being upgraded, the cluster status is **Scaling up Master node**.                                                                                                    |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Job Status
----------

:ref:`Table 2 <en-us_topic_0012799688__table792216529274>` describes the status of jobs that you execute after logging in to the MRS management console.

.. _en-us_topic_0012799688__table792216529274:

.. table:: **Table 2** Job status

   ========== ============================================================
   Status     Description
   ========== ============================================================
   Accepted   Initial status of a job after it is successfully submitted.
   Running    A job is being executed.
   Completed  A job has been executed and completed successfully.
   Terminated A job is stopped during execution.
   Abnormal   An error occurs during job execution or job execution fails.
   ========== ============================================================
