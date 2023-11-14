:original_name: mrs_02_0200.html

.. _mrs_02_0200:

Viewing Auto Scaling Policies
=============================

Function
--------

This API is used to view all auto scaling policies of a specified cluster.

URI
---

GET /v2/{project_id}/autoscaling-policy/{cluster_id}

.. table:: **Table 1** URI parameters

   +------------+-----------+--------+------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                                                      |
   +============+===========+========+==================================================================================================================+
   | project_id | Yes       | String | The project ID. For details about how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +------------+-----------+--------+------------------------------------------------------------------------------------------------------------------+
   | cluster_id | Yes       | String | The cluster ID. For details about how to obtain the cluster ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +------------+-----------+--------+------------------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

None

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 2** Response body parameter

   +-----------------+--------------------------------------+------------------------------------------------------------------------------------------------------------+
   | Parameter       | Type                                 | Description                                                                                                |
   +=================+======================================+============================================================================================================+
   | [Array element] | Array of AutoScalingPolicyV2 objects | The auto scaling policy list. For details, see :ref:`Table 3 <mrs_02_0200__response_autoscalingpolicyv2>`. |
   +-----------------+--------------------------------------+------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0200__response_autoscalingpolicyv2:

.. table:: **Table 3** AutoScalingPolicyV2

   +---------------------+--------------------------+-----------------------------------------------------------------------------------------------------+
   | Parameter           | Type                     | Description                                                                                         |
   +=====================+==========================+=====================================================================================================+
   | node_group_name     | String                   | The node group name.                                                                                |
   +---------------------+--------------------------+-----------------------------------------------------------------------------------------------------+
   | resource_pool_name  | String                   | The resource plan name.                                                                             |
   +---------------------+--------------------------+-----------------------------------------------------------------------------------------------------+
   | auto_scaling_policy | AutoScalingPolicy object | The auto scaling policy. For details, see :ref:`Table 4 <mrs_02_0200__response_autoscalingpolicy>`. |
   +---------------------+--------------------------+-----------------------------------------------------------------------------------------------------+

.. _mrs_02_0200__response_autoscalingpolicy:

.. table:: **Table 4** AutoScalingPolicy

   +---------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter           | Type                           | Description                                                                                                                                                                                                                                                                                 |
   +=====================+================================+=============================================================================================================================================================================================================================================================================================+
   | auto_scaling_enable | Boolean                        | Whether to enable the auto scaling policy.                                                                                                                                                                                                                                                  |
   +---------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | min_capacity        | Integer                        | The minimum number of nodes reserved in the node group. The value ranges from 0 to 500.                                                                                                                                                                                                     |
   +---------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | max_capacity        | Integer                        | The maximum number of nodes in the node group. The value ranges from 0 to 500.                                                                                                                                                                                                              |
   +---------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resources_plans     | Array of ResourcesPlan objects | The resource plan list. If this parameter is left blank, the resource plan is disabled. When **auto_scaling_enable** is set to **true**, either this parameter or **rules** must be configured. For details about this parameter, see :ref:`Table 5 <mrs_02_0200__response_resourcesplan>`. |
   +---------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | rules               | Array of Rule objects          | List of auto scaling rules. When **auto_scaling_enable** is set to **true**, either this parameter or **resources_plans** must be configured. For details about this parameter, see :ref:`Table 6 <mrs_02_0200__response_rule>`.                                                            |
   +---------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | exec_scripts        | Array of ScaleScript objects   | The list of custom scaling automation scripts. If this parameter is left blank, the automation script is disabled. For details, see :ref:`Table 8 <mrs_02_0200__response_scalescript>`.                                                                                                     |
   +---------------------+--------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0200__response_resourcesplan:

.. table:: **Table 5** ResourcesPlan

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                   |
   +=======================+=======================+===============================================================================================================================================================================================+
   | period_type           | String                | The cycle type of a resource plan. Currently, only the following cycle type is supported:                                                                                                     |
   |                       |                       |                                                                                                                                                                                               |
   |                       |                       | daily                                                                                                                                                                                         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | start_time            | String                | The start time of a resource plan. The value is in the format of **hour:minute**, indicating that the time ranges from 00:00 to 23:59.                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | end_time              | String                | The end time of a resource plan. The value is in the same format as that of **start_time**. The interval between **end_time** and **start_time** must be greater than or equal to 30 minutes. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | min_capacity          | Integer               | The minimum number of reserved nodes in a node group in a resource plan. The value ranges from 0 to 500.                                                                                      |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | max_capacity          | Integer               | The maximum number of reserved nodes in a node group in a resource plan. The value ranges from 0 to 500.                                                                                      |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | effective_days        | Array of strings      | Effective date of a resource plan. If this parameter is left blank, it indicates that the resource plan takes effect every day. The options are as follows:                                   |
   |                       |                       |                                                                                                                                                                                               |
   |                       |                       | **MONDAY**, **TUESDAY**, **WEDNESDAY**, **THURSDAY**, **FRIDAY**, **SATURDAY**, and **SUNDAY**                                                                                                |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0200__response_rule:

.. table:: **Table 6** Rule

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                               |
   +=======================+=======================+===========================================================================================================================================================================================================+
   | name                  | String                | The name of an auto scaling rule. The name can contain only 1 to 64 characters. Only letters, numbers, hyphens (-), and underscores (_) are allowed. Rule names must be unique in a node group.           |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | description           | String                | The description about an auto scaling rule. It contains a maximum of 1,024 characters.                                                                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | adjustment_type       | String                | Auto scaling rule adjustment type. Possible values:                                                                                                                                                       |
   |                       |                       |                                                                                                                                                                                                           |
   |                       |                       | -  **scale_out**: cluster scale-out                                                                                                                                                                       |
   |                       |                       | -  **scale_in**: cluster scale-in                                                                                                                                                                         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cool_down_minutes     | Integer               | The cluster cooling time after an auto scaling rule is triggered, when no auto scaling operation is performed. The unit is minute. The value ranges from 0 to 10080. One week is equal to 10,080 minutes. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | scaling_adjustment    | Integer               | The number of cluster nodes that can be adjusted at a time. The value ranges from 1 to 100.                                                                                                               |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | trigger               | Trigger object        | The condition for triggering a rule. For details, see :ref:`Table 7 <mrs_02_0200__response_trigger>`.                                                                                                     |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0200__response_trigger:

.. table:: **Table 7** Trigger

   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                          |
   +=======================+=======================+======================================================================================================================================================+
   | metric_name           | String                | The metric name. This triggering condition makes a judgment according to the value of the metric. A metric name contains a maximum of 64 characters. |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | metric_value          | String                | The metric threshold to trigger a rule.                                                                                                              |
   |                       |                       |                                                                                                                                                      |
   |                       |                       | The value must be an integer or a number with two decimal places.                                                                                    |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | comparison_operator   | String                | The metric judgment logic operator. Possible values:                                                                                                 |
   |                       |                       |                                                                                                                                                      |
   |                       |                       | -  **LT**: less than                                                                                                                                 |
   |                       |                       | -  **GT**: greater than                                                                                                                              |
   |                       |                       | -  **LTOE**: less than or equal to                                                                                                                   |
   |                       |                       | -  **GTOE**: greater than or equal to                                                                                                                |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
   | evaluation_periods    | Integer               | The number of consecutive five-minute periods, during which a metric threshold is reached. The value ranges from 1 to 288.                           |
   +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0200__response_scalescript:

.. table:: **Table 8** ScaleScript

   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                                               |
   +=======================+=======================+===========================================================================================================================================================================================================================================+
   | name                  | String                | The name of a custom automation script. Names must be unique in a cluster. The value can contain only numbers, letters, spaces, hyphens (-), and underscores (_) and cannot start with a space. The value can contain 1 to 64 characters. |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | uri                   | String                | The path of a custom automation script. Set this parameter to an OBS bucket path or a local VM path.                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                                                           |
   |                       |                       | -  OBS bucket path: Enter a script path, for example, **obs://**\ *XXX*\ **/scale.sh**.                                                                                                                                                   |
   |                       |                       | -  Local VM path: Enter a script path. The script path must start with a slash (/) and end with **.sh**.                                                                                                                                  |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | parameters            | String                | Parameters of a custom automation script. Multiple parameters are separated by space. The following predefined system parameters can be transferred:                                                                                      |
   |                       |                       |                                                                                                                                                                                                                                           |
   |                       |                       | -  *${mrs_scale_node_num}*: The number of nodes to be added or removed                                                                                                                                                                    |
   |                       |                       | -  *${mrs_scale_type}*: The scaling type. The value can be **scale_out** or **scale_in**.                                                                                                                                                 |
   |                       |                       | -  *${mrs_scale_node_hostnames}*: Host names of the nodes to be added or removed                                                                                                                                                          |
   |                       |                       | -  *${mrs_scale_node_ips}*: IP addresses of the nodes to be added or removed                                                                                                                                                              |
   |                       |                       | -  *${mrs_scale_rule_name}*: The name of the rule that triggers scaling. Other user-defined parameters are used in the same way as those of common shell scripts. Parameters are separated by spaces.                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | nodes                 | Array of strings      | The name of the node group where the custom automation script is executed.                                                                                                                                                                |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | active_master         | Boolean               | Whether the custom automation script runs only on the active master node. The default value is **false**, indicating that the custom automation script can run on all master nodes.                                                       |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | fail_action           | String                | Whether to continue executing subsequent scripts and creating a cluster after the custom automation script fails to execute. Notes:                                                                                                       |
   |                       |                       |                                                                                                                                                                                                                                           |
   |                       |                       | -  You are advised to set this parameter to **continue** in the commissioning phase so the cluster can continue to be installed and started no matter whether the custom automation script is executed successfully.                      |
   |                       |                       | -  The scale-in operation cannot be undone. **fail_action** must be set to **continue** for the scripts that are executed after scale-in. Possible values:                                                                                |
   |                       |                       | -  **continue**: Continue to execute subsequent scripts.                                                                                                                                                                                  |
   |                       |                       | -  **errorout**: Stop the action.                                                                                                                                                                                                         |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | action_stage          | String                | The time when a script is executed. Possible values:                                                                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                                                           |
   |                       |                       | -  **before_scale_out**: before scale-out                                                                                                                                                                                                 |
   |                       |                       | -  **before_scale_in**: before scale-in                                                                                                                                                                                                   |
   |                       |                       | -  **after_scale_out**: after scale-out                                                                                                                                                                                                   |
   |                       |                       | -  **after_scale_in**: after scale-in                                                                                                                                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 9** Response body parameters

   ========== ====== ==================
   Parameter  Type   Description
   ========== ====== ==================
   error_code String Error codes.
   error_msg  String The error message.
   ========== ====== ==================

Example Request
---------------

None

Example Response
----------------

**Status code: 200**

Auto scaling policies are displayed.

.. code-block::

   {
     "auto_scaling_policies" : [ {
       "node_group_name" : "task_node_analysis_group",
       "resource_pool_name" : "default",
       "auto_scaling_policy" : {
         "auto_scaling_enable" : true,
         "min_capacity" : 0,
         "max_capacity" : 1,
         "resources_plans" : [ {
           "period_type" : "daily",
           "effective_days" : [ "SUNDAY" ],
           "start_time" : "12:00",
           "end_time" : "13:00",
           "min_capacity" : 2,
           "max_capacity" : 3
         } ],
         "rules" : [ {
           "name" : "default-expand-1",
           "description" : "",
           "adjustment_type" : "scale_out",
           "cool_down_minutes" : 5,
           "scaling_adjustment" : 1,
           "trigger" : {
             "metric_name" : "YARNAppRunning",
             "metric_value" : 100,
             "comparison_operator" : "GTOE",
             "evaluation_periods" : 1
           }
         } ]
       }
     } ]
   }

Status Codes
------------

See :ref:`Status Codes <mrs_02_0015>`.

Error Codes
-----------

See :ref:`Error Code <mrs_02_0014>`.
