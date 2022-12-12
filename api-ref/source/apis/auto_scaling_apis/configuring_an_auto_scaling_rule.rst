:original_name: mrs_02_0056.html

.. _mrs_02_0056:

Configuring an Auto Scaling Rule
================================

Function
--------

This API is used to configure an auto scaling rule.

The API used for cluster creation and job execution can also be used to create an auto scaling rule.

URI
---

-  Format

   POST /v1.1/{project_id}/autoscaling-policy/{cluster_id}

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Parameter  | Mandatory | Description                                                                                               |
      +============+===========+===========================================================================================================+
      | project_id | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | cluster_id | Yes       | Cluster ID                                                                                                |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

:ref:`Table 2 <mrs_02_0056__table27243156151210>` and :ref:`Table 3 <mrs_02_0056__table50379282141720>` describe the request parameters.

.. _mrs_02_0056__table27243156151210:

.. table:: **Table 2** **node_group** parameter description

   +------------+-----------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                                                                                                               |
   +============+===========+========+===========================================================================================================================================================================+
   | node_group | Yes       | String | Type of the node to which an auto scaling rule applies. Currently, only Task nodes support auto scaling rules, that is, the request value is **task_node_default_group**. |
   +------------+-----------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0056__table50379282141720:

.. table:: **Table 3** **auto_scaling_policy** parameter description

   +---------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter           | Mandatory       | Type            | Description                                                                                                                                                                              |
   +=====================+=================+=================+==========================================================================================================================================================================================+
   | auto_scaling_enable | Yes             | Boolean         | Whether to enable the auto scaling rule.                                                                                                                                                 |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | min_capacity        | Yes             | Integer         | Minimum number of nodes left in the node group.                                                                                                                                          |
   |                     |                 |                 |                                                                                                                                                                                          |
   |                     |                 |                 | Value range: 0 to 500                                                                                                                                                                    |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | max_capacity        | Yes             | Integer         | Maximum number of nodes in the node group.                                                                                                                                               |
   |                     |                 |                 |                                                                                                                                                                                          |
   |                     |                 |                 | Value range: 0 to 500                                                                                                                                                                    |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resources_plans     | No              | List            | Resource plan list. For details, see :ref:`Table 4 <mrs_02_0056__table1979310416120>`. If this parameter is left blank, the resource plan is disabled.                                   |
   |                     |                 |                 |                                                                                                                                                                                          |
   |                     |                 |                 | When auto scaling is enabled, either a resource plan or an auto scaling rule must be configured.                                                                                         |
   |                     |                 |                 |                                                                                                                                                                                          |
   |                     |                 |                 | MRS 1.6.3 or later supports this parameter.                                                                                                                                              |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | exec_scripts        | No              | List            | List of custom scaling automation scripts. For details, see :ref:`Table 5 <mrs_02_0056__tefd2eb7c7838496eadbf4b310193de4a>`. If this parameter is left blank, a hook script is disabled. |
   |                     |                 |                 |                                                                                                                                                                                          |
   |                     |                 |                 | MRS 1.7.2 or later supports this parameter.                                                                                                                                              |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | rules               | No              | List            | List of auto scaling rules. For details, see :ref:`Table 6 <mrs_02_0056__t46230cdbc4f641f6b17d64de5747728b>`.                                                                            |
   |                     |                 |                 |                                                                                                                                                                                          |
   |                     |                 |                 | When auto scaling is enabled, either a resource plan or an auto scaling rule must be configured.                                                                                         |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0056__table1979310416120:

.. table:: **Table 4** **resources_plan** parameter description

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                               |
   +=================+=================+=================+===========================================================================================================================================================================================+
   | period_type     | Yes             | String          | Cycle type of a resource plan. Currently, only the following cycle type is supported:                                                                                                     |
   |                 |                 |                 |                                                                                                                                                                                           |
   |                 |                 |                 | -  daily                                                                                                                                                                                  |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | start_time      | Yes             | String          | Start time of a resource plan. The value is in the format of **hour:minute**, indicating that the time ranges from 0:00 to 23:59.                                                         |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | end_time        | Yes             | String          | End time of a resource plan. The value is in the same format as that of **start_time**. The interval between **end_time** and **start_time** must be greater than or equal to 30 minutes. |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | min_capacity    | Yes             | Integer         | Minimum number of the preserved nodes in a node group in a resource plan.                                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                           |
   |                 |                 |                 | Value range: 0 to 500                                                                                                                                                                     |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | max_capacity    | Yes             | Integer         | Maximum number of the preserved nodes in a node group in a resource plan.                                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                           |
   |                 |                 |                 | Value range: 0 to 500                                                                                                                                                                     |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0056__tefd2eb7c7838496eadbf4b310193de4a:

.. table:: **Table 5** **exec_script** parameter description

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                     |
   +=================+=================+=================+=================================================================================================================================================================================================================================+
   | name            | Yes             | String          | Name of a custom automation script. It must be unique in a same cluster.                                                                                                                                                        |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | The value can contain only digits, letters, spaces, hyphens (-), and underscores (_) and must not start with a space.                                                                                                           |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | The value can contain 1 to 64 characters.                                                                                                                                                                                       |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | uri             | Yes             | String          | Path of a custom automation script. Set this parameter to an OBS bucket path or a local VM path.                                                                                                                                |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  OBS bucket path: Enter a script path manually. for example, **s3a://**\ *XXX*\ **/scale.sh**.                                                                                                                                |
   |                 |                 |                 | -  Local VM path: Enter a script path. The script path must start with a slash (/) and end with **.sh**.                                                                                                                        |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | parameters      | No              | String          | Parameters of a custom automation script.                                                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  Multiple parameters are separated by space.                                                                                                                                                                                  |
   |                 |                 |                 | -  The following predefined system parameters can be transferred:                                                                                                                                                               |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 |    -  *${mrs_scale_node_num}*: Number of the nodes to be added or removed                                                                                                                                                       |
   |                 |                 |                 |    -  *${mrs_scale_type}*: Scaling type. The value can be **scale_out** or **scale_in**.                                                                                                                                        |
   |                 |                 |                 |    -  *${mrs_scale_node_hostnames}*: Host names of the nodes to be added or removed                                                                                                                                             |
   |                 |                 |                 |    -  *${mrs_scale_node_ips}*: IP addresses of the nodes to be added or removed                                                                                                                                                 |
   |                 |                 |                 |    -  *${mrs_scale_rule_name}*: Name of the rule that triggers auto scaling                                                                                                                                                     |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  Other user-defined parameters are used in the same way as those of common shell scripts. Parameters are separated by space.                                                                                                  |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | nodes           | Yes             | List<String>    | Type of a node where the custom automation script is executed. The node type can be Master, Core, or Task.                                                                                                                      |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | active_master   | No              | Boolean         | Whether the custom automation script runs only on the active Master node.                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | The default value is **false**, indicating that the custom automation script can run on all Master nodes.                                                                                                                       |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | action_stage    | Yes             | String          | Time when a script is executed.                                                                                                                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | The following four options are supported:                                                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  **before_scale_out**: before scale-out                                                                                                                                                                                       |
   |                 |                 |                 | -  **before_scale_in**: before scale-in                                                                                                                                                                                         |
   |                 |                 |                 | -  **after_scale_out**: after scale-out                                                                                                                                                                                         |
   |                 |                 |                 | -  **after_scale_in**: after scale-in                                                                                                                                                                                           |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | fail_action     | Yes             | String          | Whether to continue to execute subsequent scripts and create a cluster after the custom automation script fails to be executed.                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  **continue**: Continue to execute subsequent scripts.                                                                                                                                                                        |
   |                 |                 |                 | -  **errorout**: Stop the action.                                                                                                                                                                                               |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 |    .. note::                                                                                                                                                                                                                    |
   |                 |                 |                 |                                                                                                                                                                                                                                 |
   |                 |                 |                 |       -  You are advised to set this parameter to **continue** in the commissioning phase so that the cluster can continue to be installed and started no matter whether the custom automation script is executed successfully. |
   |                 |                 |                 |       -  The scale-in operation cannot be undone. Therefore, **fail_action** must be set to **continue** for the scripts that are executed after scale-in.                                                                      |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0056__t46230cdbc4f641f6b17d64de5747728b:

.. table:: **Table 6** **rules** parameter description

   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | Parameter          | Mandatory       | Type            | Description                                                                                                                    |
   +====================+=================+=================+================================================================================================================================+
   | name               | Yes             | String          | Name of an auto scaling rule.                                                                                                  |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | A cluster name can contain only 1 to 64 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed.        |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | Rule names must be unique in a node group.                                                                                     |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | description        | No              | String          | Description about an auto scaling rule.                                                                                        |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | It contains a maximum of 1,024 characters.                                                                                     |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | adjustment_type    | Yes             | String          | Auto scaling rule adjustment type. The options are as follows:                                                                 |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | -  **scale_out**: cluster scale-out                                                                                            |
   |                    |                 |                 | -  **scale_in**: cluster scale-in                                                                                              |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | cool_down_minutes  | Yes             | Integer         | Cluster cooling time after an auto scaling rule is triggered, when no auto scaling operation is performed. The unit is minute. |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | Value range: 0 to 10,080. One week is equal to 10,080 minutes.                                                                 |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | scaling_adjustment | Yes             | Integer         | Number of nodes that can be adjusted once.                                                                                     |
   |                    |                 |                 |                                                                                                                                |
   |                    |                 |                 | Value range: 1 to 100                                                                                                          |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+
   | trigger            | Yes             | Trigger         | Condition for triggering a rule. For details, see :ref:`Table 7 <mrs_02_0056__tb0fcdad7ce8f4ebdb4fd9e76d805b5e8>`.             |
   +--------------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0056__tb0fcdad7ce8f4ebdb4fd9e76d805b5e8:

.. table:: **Table 7** **trigger** parameter description

   +---------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter           | Mandatory       | Type            | Description                                                                                                                                                                                                      |
   +=====================+=================+=================+==================================================================================================================================================================================================================+
   | metric_name         | Yes             | String          | Metric name.                                                                                                                                                                                                     |
   |                     |                 |                 |                                                                                                                                                                                                                  |
   |                     |                 |                 | This triggering condition makes a judgment according to the value of the metric.                                                                                                                                 |
   |                     |                 |                 |                                                                                                                                                                                                                  |
   |                     |                 |                 | A metric name contains a maximum of 64 characters.                                                                                                                                                               |
   |                     |                 |                 |                                                                                                                                                                                                                  |
   |                     |                 |                 | :ref:`Table 8 <mrs_02_0056__td49a8d90c5444d929b277b709d35c445>` lists the supported metric names.                                                                                                                |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | metric_value        | Yes             | String          | Metric threshold to trigger a rule                                                                                                                                                                               |
   |                     |                 |                 |                                                                                                                                                                                                                  |
   |                     |                 |                 | The parameter value must be an integer or number with two decimal places only. :ref:`Table 8 <mrs_02_0056__td49a8d90c5444d929b277b709d35c445>` provides value types and ranges corresponding to **metric_name**. |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | comparison_operator | No              | String          | Metric judgment logic operator. The options are as follows:                                                                                                                                                      |
   |                     |                 |                 |                                                                                                                                                                                                                  |
   |                     |                 |                 | -  **LT**: less than                                                                                                                                                                                             |
   |                     |                 |                 | -  **GT**: greater than                                                                                                                                                                                          |
   |                     |                 |                 | -  **LTOE**: less than or equal to                                                                                                                                                                               |
   |                     |                 |                 | -  **GTOE**: greater than or equal to                                                                                                                                                                            |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | evaluation_periods  | Yes             | Integer         | Number of consecutive five-minute periods, during which a metric threshold is reached                                                                                                                            |
   |                     |                 |                 |                                                                                                                                                                                                                  |
   |                     |                 |                 | Value range: 1 to 288                                                                                                                                                                                            |
   +---------------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0056__td49a8d90c5444d929b277b709d35c445:

.. table:: **Table 8** Auto scaling metrics

   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   | Cluster Type      | Metric                                   | Value Type      | Description                                                                                                  |
   +===================+==========================================+=================+==============================================================================================================+
   | Streaming cluster | StormSlotAvailable                       | Integer         | Number of available Storm slots.                                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSlotAvailablePercentage             | Percentage      | Percentage of available Storm slots, that is, the proportion of the available slots to total slots.          |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100.                                                                                       |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSlotUsed                            | Integer         | Number of the used Storm slots.                                                                              |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSlotUsedPercentage                  | Percentage      | Percentage of the used Storm slots, that is, the proportion of the used slots to total slots.                |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100.                                                                                       |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSupervisorMemAverageUsage           | Integer         | Average memory usage of the Supervisor process of Storm.                                                     |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSupervisorMemAverageUsagePercentage | Percentage      | Average percentage of the used memory of the Supervisor process of Storm to the total memory of the system.  |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100.                                                                                       |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | StormSupervisorCPUAverageUsagePercentage | Percentage      | Average percentage of the used CPUs of the Supervisor process of Storm to the total CPUs.                    |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 6000.                                                                                      |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   | Analysis cluster  | YARNAppPending                           | Integer         | Number of pending tasks on Yarn.                                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNAppPendingRatio                      | Ratio           | Ratio of pending tasks on Yarn, that is, the ratio of pending tasks to running tasks on Yarn.                |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNAppRunning                           | Integer         | Number of running tasks on Yarn.                                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNContainerAllocated                   | Integer         | Number of containers allocated to Yarn.                                                                      |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNContainerPending                     | Integer         | Number of pending containers on Yarn.                                                                        |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNContainerPendingRatio                | Ratio           | Ratio of pending containers on Yarn, that is, the ratio of pending containers to running containers on Yarn. |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUAllocated                         | Integer         | Number of virtual CPUs (vCPUs) allocated to Yarn                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUAvailable                         | Integer         | Number of available vCPUs on Yarn.                                                                           |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUAvailablePercentage               | Percentage      | Percentage of available vCPUs on Yarn, that is, the proportion of available vCPUs to total vCPUs.            |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100.                                                                                       |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNCPUPending                           | Integer         | Number of pending vCPUs on Yarn.                                                                             |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryAllocated                      | Integer         | Memory allocated to Yarn. The unit is MB.                                                                    |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryAvailable                      | Integer         | Available memory on Yarn. The unit is MB.                                                                    |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryAvailablePercentage            | Percentage      | Percentage of available memory on Yarn, that is, the proportion of available memory to total memory on Yarn. |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 100.                                                                                       |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+
   |                   | YARNMemoryPending                        | Integer         | Pending memory on Yarn.                                                                                      |
   |                   |                                          |                 |                                                                                                              |
   |                   |                                          |                 | Value range: 0 to 2147483646.                                                                                |
   +-------------------+------------------------------------------+-----------------+--------------------------------------------------------------------------------------------------------------+

.. note::

   When the value type is percentage or ratio in :ref:`Table 8 <mrs_02_0056__td49a8d90c5444d929b277b709d35c445>`, the valid value can be accurate to percentile. The percentage metric value is a decimal value with a percent sign (%) removed. For example, 16.80 represents 16.80%.

Response
--------

.. table:: **Table 9** Response parameter description

   +-----------------------+-----------------------+--------------------------------------------+
   | Parameter             | Type                  | Description                                |
   +=======================+=======================+============================================+
   | result                | String                | Operation result                           |
   |                       |                       |                                            |
   |                       |                       | -  succeeded: The operation is successful. |
   +-----------------------+-----------------------+--------------------------------------------+

Example
-------

-  Example request

   .. code-block::

      {
        "node_group":"task_node_default_group",
        "auto_scaling_policy": {
            "auto_scaling_enable": true,
            "min_capacity": "1",
            "max_capacity": "3",
            "resources_plans": [{
               "period_type": "daily",
               "start_time": "9:50",
               "end_time": "10:20",
               "min_capacity": "2",
               "max_capacity": "3"
               },{
               "period_type": "daily",
               "start_time": "10:20",
               "end_time": "12:30",
               "min_capacity": "0",
               "max_capacity": "2"
             }],
             "exec_scripts": [{
               "name": "before_scale_out",
               "uri": "s3a://XXX/zeppelin_install.sh",
               "parameters": "",
               "nodes": [
                 "master",
                 "core",
                 "task"
               ],
               "active_master": "true",
               "action_stage": "before_scale_out",
               "fail_action": "continue"
               },{
               "name": "after_scale_out",
               "uri": "s3a://XXX/storm_rebalance.sh",
               "parameters": "",
               "nodes": [
                 "master",
                 "core",
                 "task"
               ],
               "active_master": "true",
               "action_stage": "after_scale_out",
               "fail_action": "continue"
            }],
            "rules": [{
               "name": "default-expand-1",
               "adjustment_type": "scale_out",
               "cool_down_minutes": 5,
               "scaling_adjustment": 1,
               "trigger": {
                  "metric_name": "YARNMemoryAvailablePercentage",
                  "metric_value": "25",
                  "comparison_operator": "LT",
                  "evaluation_periods": 10
                  }
                },
               {
                "name": "default-shrink-1",
                "adjustment_type": "scale_in",
                "cool_down_minutes": 5,
                "scaling_adjustment": 1,
                "trigger": {
                   "metric_name": "YARNMemoryAvailablePercentage",
                   "metric_value": "70",
                   "comparison_operator": "GT",
                   "evaluation_periods": 10
                    }
                 }]
           }
      }

   .. note::

      A new auto scaling rule will overwrite the auto scaling rule saved in the original database. If you want to modify the original rule, query the original rule first, modify the rule, and submit a modification task. For details, see :ref:`Querying Cluster Details <mrs_02_0031>`.

-  Example response

   .. code-block::

      {       "result": "succeeded"  }

Status Code
-----------

:ref:`Table 10 <mrs_02_0056__table5043525610328>` describes the status code of this API.

.. _mrs_02_0056__table5043525610328:

.. table:: **Table 10** Status code

   =========== ==========================================
   Status Code Description
   =========== ==========================================
   200         The cluster has been successfully created.
   =========== ==========================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
