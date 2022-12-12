:original_name: mrs_02_0029.html

.. _mrs_02_0029:

Resizing a Cluster
==================

Function
--------

This API is used to manually scale out or scale in Core or Task nodes in a cluster that has been created. After an MRS cluster is created, the number of Master nodes cannot be adjusted. That is, Master nodes cannot be scaled in or out. This API is incompatible with Sahara.

Only clusters in the **Running** state can be scaled out or in.

URI
---

-  Format

   PUT /v1.1/{project_id}/cluster_infos/{cluster_id}

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

.. table:: **Table 2** Request parameter description

   +------------+-----------+--------+----------------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                                  |
   +============+===========+========+==============================================================================================+
   | service_id | No        | String | Service ID. This parameter is reserved for extension. You do not need to set this parameter. |
   +------------+-----------+--------+----------------------------------------------------------------------------------------------+
   | plan_id    | No        | String | Plan ID. This parameter is reserved for extension. You do not need to set this parameter.    |
   +------------+-----------+--------+----------------------------------------------------------------------------------------------+
   | parameters | Yes       | Object | Core parameters. For details, see :ref:`Table 3 <mrs_02_0029__table19445385114112>`.         |
   +------------+-----------+--------+----------------------------------------------------------------------------------------------+

.. _mrs_02_0029__table19445385114112:

.. table:: **Table 3** **parameters** description

   +------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter              | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                                            |
   +========================+=================+=================+========================================================================================================================================================================================================================================================================================================================================================================================+
   | order_id               | No              | String          | Order ID obtained by the system during scale-out or scale-in. You do not need to set the parameter.                                                                                                                                                                                                                                                                                    |
   +------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | scale_type             | Yes             | String          | -  **scale_in**: cluster scale-in                                                                                                                                                                                                                                                                                                                                                      |
   |                        |                 |                 | -  **scale_out**: cluster scale-out                                                                                                                                                                                                                                                                                                                                                    |
   +------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_id                | Yes             | String          | ID of the newly added or removed node. The parameter value is fixed to **node_orderadd**. The ID of a newly added or removed node includes **node_orderadd**, for example, **node-orderadd-TBvSr.com**.                                                                                                                                                                                |
   +------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | node_group             | No              | String          | Node group to be scaled out or in                                                                                                                                                                                                                                                                                                                                                      |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                 | -  If the value of **node_group** is **core_node_default_group**, the node group is a Core node group.                                                                                                                                                                                                                                                                                 |
   |                        |                 |                 | -  If the value of **node_group** is **task_node_default_group**, the node group is a Task node group.                                                                                                                                                                                                                                                                                 |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                 | If it is left blank, the default value **core_node_default_group** is used.                                                                                                                                                                                                                                                                                                            |
   +------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | task_node_info         | No              | Object          | Task node specifications. For more parameter description, see :ref:`Table 5 <mrs_02_0029__table629219569398>`.                                                                                                                                                                                                                                                                         |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                 | -  When the number of Task nodes is **0**, this parameter is used to specify Task node specifications.                                                                                                                                                                                                                                                                                 |
   |                        |                 |                 | -  When the number of Task nodes is greater than **0**, this parameter is unavailable.                                                                                                                                                                                                                                                                                                 |
   +------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | instances              | Yes             | String/Integer  | Number of nodes to be added or removed                                                                                                                                                                                                                                                                                                                                                 |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                 | -  The maximum number of nodes to be added is 500 minus the number of Core and Task nodes. For example, the current number of Core nodes is 3, the number of nodes to be added must be less than or equal to 497.                                                                                                                                                                      |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                 |    A maximum of 500 Core and Task nodes are supported by default. If more than 500 Core and Task nodes are required, contact technical support engineers or call a background API to modify the database.                                                                                                                                                                              |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                 | -  Nodes can be deleted for cluster scale-out when the number of Core nodes is greater than 3 or the number of Task nodes is greater than 0. For example, if there are 5 Core nodes and 5 Task nodes in a cluster, only 2 (5 minus 3) Core nodes are available for deletion and 5 or fewer than 5 Task nodes can be deleted.                                                           |
   +------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | skip_bootstrap_scripts | No              | Boolean         | This parameter is valid only when a bootstrap action is configured during cluster creation and takes effect during scale-out. It indicates whether the bootstrap action specified during cluster creation is performed on nodes added during scale-out. The default value is **false**, indicating that the bootstrap action is performed. MRS 1.7.2 or later supports this parameter. |
   +------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | scale_without_start    | No              | boolean         | Whether to start components on the added nodes after cluster scale-out                                                                                                                                                                                                                                                                                                                 |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                 | -  **true**: Do not start components after scale-out.                                                                                                                                                                                                                                                                                                                                  |
   |                        |                 |                 | -  **false**: Start components after scale-out.                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                 | This parameter is valid only in MRS 1.7.2 or later.                                                                                                                                                                                                                                                                                                                                    |
   +------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | server_ids             | No              | List<String>    | ID list of Task nodes to be deleted during task node scale-in.                                                                                                                                                                                                                                                                                                                         |
   |                        |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                        |
   |                        |                 |                 | -  This parameter does not take effect when **scale_type** is set to **scale-out**.                                                                                                                                                                                                                                                                                                    |
   |                        |                 |                 | -  If **scale_type** is set to **scale-in** and cannot be left blank, the system deletes the specified Task nodes.                                                                                                                                                                                                                                                                     |
   |                        |                 |                 | -  When **scale_type** is set to **scale-in** and **server_ids** is left blank, the system automatically deletes the Task nodes based on the system rules.                                                                                                                                                                                                                             |
   +------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | previous_values        | No              | Object          | Extension parameter. You do not need to set this parameter. For details, see :ref:`Table 4 <mrs_02_0029__table1718927182716>`.                                                                                                                                                                                                                                                         |
   +------------------------+-----------------+-----------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0029__table1718927182716:

.. table:: **Table 4** Parameter description of **previous_values**

   +-----------------+-----------------+-----------------+-------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                               |
   +=================+=================+=================+===========================================+
   | plan_id         | No              | String          | Reserve the parameter for extending APIs. |
   |                 |                 |                 |                                           |
   |                 |                 |                 | You do not need to set the parameter.     |
   +-----------------+-----------------+-----------------+-------------------------------------------+

.. _mrs_02_0029__table629219569398:

.. table:: **Table 5** **task_node_info** parameter description

   +-------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | Parameter         | Mandatory       | Type            | Description                                                                                         |
   +===================+=================+=================+=====================================================================================================+
   | node_size         | Yes             | String          | Instance specifications of a Task node, for example, c6.4xlarge.4linux.mrs                          |
   |                   |                 |                 |                                                                                                     |
   |                   |                 |                 | For details about instance specifications, see :ref:`ECS Specifications Used by MRS <mrs_01_9005>`. |
   +-------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | data_volume_type  | No              | String          | Data disk storage type of the Task node, supporting SATA, SAS, and SSD currently                    |
   |                   |                 |                 |                                                                                                     |
   |                   |                 |                 | -  SATA: Common I/O                                                                                 |
   |                   |                 |                 | -  SAS: High I/O                                                                                    |
   |                   |                 |                 | -  SSD: Ultra-high I/O                                                                              |
   +-------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | data_volume_count | No              | Integer         | Number of data disks of a Task node                                                                 |
   |                   |                 |                 |                                                                                                     |
   |                   |                 |                 | Value range: 1 to 10                                                                                |
   +-------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | data_volume_size  | No              | Integer         | Data disk storage space of a Task node                                                              |
   |                   |                 |                 |                                                                                                     |
   |                   |                 |                 | Value range: 100 GB to 32,000 GB                                                                    |
   +-------------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+

Response
--------

**Response parameters**

:ref:`Table 6 <mrs_02_0029__table8319691114112>` describes the response parameters.

.. _mrs_02_0029__table8319691114112:

.. table:: **Table 6** Response parameter description

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                    |
   +=======================+=======================+================================================================================================================+
   | result                | String                | Operation result                                                                                               |
   |                       |                       |                                                                                                                |
   |                       |                       | -  **succeeded**: The operation is successful.                                                                 |
   |                       |                       | -  :ref:`Table 8 <mrs_02_0029__table101661350414>` describes the error codes returned upon operation failures. |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   Scaling out Core nodes:

   .. code-block::

      {
          "service_id": "",
          "plan_id": "",
          "parameters": {
              "order_id": "",
              "scale_type": "scale_out",
              "node_id": "node_orderadd",
              "node_group": "core_node_default_group",
              "instances": "1",
             "skip_bootstrap_scripts":false,
             "scale_without_start":false
          },
          "previous_values": {
              "plan_id": ""
          }
      }

   Scaling out Task nodes when the number of the existing Task nodes is greater than zero:

   .. code-block::

      {
          "service_id": "",
          "plan_id": "",
          "parameters": {
              "order_id": "",
              "scale_type": "scale_out",
              "node_id": "node_orderadd",
              "node_group": "task_node_default_group",
              "instances": "1",
              "skip_bootstrap_scripts":false,
              "scale_without_start":false
          },
          "previous_values": {
              "plan_id": ""
          }
      }

   Scaling out Task nodes when the number of the existing Task nodes is zero:

   .. code-block::

      {
          "service_id": "",
          "plan_id": "",
          "parameters": {
              "order_id": "",
              "scale_type": "scale_out",
              "node_id": "node_orderadd",
              "node_group": "task_node_default_group",
              "task_node_info": {
                        "node_size": "s1.xlarge.linux.mrs",
                        "data_volume_type":"SATA",
                        "data_volume_count":2,
                        "data_volume_size":200
                        },
              "instances": "1",
              "scale_without_start":false


          },
          "previous_values": {
              "plan_id": ""
          }
      }

   Scaling in Core nodes:

   .. code-block::

      {
          "service_id": "",
          "plan_id": "",
          "parameters": {
              "order_id": "",
              "scale_type": "scale_in",
              "node_id": "node_orderadd",
              "node_group": "core_node_default_group",
              "instances": "1"


          },
          "previous_values": {
              "plan_id": ""
          }
      }

   Scaling in Task nodes:

   .. code-block::

      {
          "service_id": "",
          "plan_id": "",
          "parameters": {
              "order_id": "",
              "scale_type": "scale_in",
              "node_id": "node_orderadd",
              "node_group": "task_node_default_group",
              "instances": "1"


          },
          "previous_values": {
              "plan_id": ""
          }
      }

   The following is an example of a specified Task node scale-in:

   .. code-block::

      {
          "service_id": "",
          "plan_id": "",
          "parameters": {
              "order_id": "",
              "scale_type": "scale_in",
              "node_id": "node_orderadd",
              "node_group": "task_node_default_group",
              "instances": "2",
              "server_ids": ["c9573435-7814-4b2c-9131-ad78b814414c", "a4951009-6a0f-4e7b-9c81-9d4bd1f8c537"]
          },
          "previous_values": {
              "plan_id": ""
          }
      }

-  Example response

   .. code-block::

      {
          "result": "succeeded"
      }

Status Code
-----------

-  :ref:`Table 7 <mrs_02_0029__table60948494114112>` describes the status code of this API.

   .. _mrs_02_0029__table60948494114112:

   .. table:: **Table 7** Status code

      +-------------+-----------------------------------------------------------------+
      | Status Code | Description                                                     |
      +=============+=================================================================+
      | 200         | The Core or Task nodes have been successfully scaled out or in. |
      +-------------+-----------------------------------------------------------------+

-  :ref:`Table 8 <mrs_02_0029__table101661350414>` describes the error codes returned upon operation failures.

   .. _mrs_02_0029__table101661350414:

   .. table:: **Table 8** Error codes

      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | Error Code | Message                                                                                                                  |
      +============+==========================================================================================================================+
      | 12000001   | Identity verification is invalid                                                                                         |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000002   | The parameter is invalid.                                                                                                |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000003   | The cluster does not exist.                                                                                              |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000009   | The method parameter is invalid.                                                                                         |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000013   | Scale-in of cluster *XX* failed.                                                                                         |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000014   | Scale-out of cluster *XX* failed.                                                                                        |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000017   | Scale-out or scale-in is not allowed for clusters that are not in the **Running** state.                                 |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000018   | Scale-out or scale-in cannot be performed again because it is in progress.                                               |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000019   | Failed to obtain hosts of the cluster.                                                                                   |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000028   | The maximum number of Core nodes in a cluster is *N*.                                                                    |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000029   | Failed to obtain the quota.                                                                                              |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000030   | The requested number of nodes in the cluster exceeds the available quota.                                                |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000031   | The requested number of vCPUs in the cluster exceeds the available quota.                                                |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000032   | The requested memory of the cluster exceeds the available quota.                                                         |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000033   | The requested number of disks in the cluster exceeds the available quota.                                                |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000034   | The requested disk capacity of the cluster exceeds the available quota.                                                  |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000054   | The operation is not supported.                                                                                          |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000067   | The cluster cannot be scaled out because its version is too early. Upgrade the cluster to the latest version.            |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000068   | The status of some nodes is not running in the cluster. Try again later.                                                 |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | 12000121   | Scale-out is not allowed because the cluster has an unpaid order. Scale out the cluster again after you pay the order.   |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | MRS.101    | Your request could not be fulfilled because your quota is insufficient. Contact technical support to increase the quota. |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | MRS.102    | The token cannot be null or invalid. Try again later or contact customer service.                                        |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | MRS.103    | Invalid request. Try again later or contact customer service.                                                            |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | MRS.104    | Insufficient resources. Try again later or contact customer service.                                                     |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | MRS.105    | Insufficient IP addresses in the existing subnet. Try again later or contact customer service.                           |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | MRS.201    | Failed due to an ECS error. Try again later or contact customer service. (ECS: *xxxx*, ECS error information)            |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | MRS.202    | Failed due to an IAM error. Try again later or contact customer service. (IAM: *xxxx*, IAM error information)            |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | MRS.203    | Failed due to a VPC error. Try again later or contact customer service. (VPC: *xxxx*, VPC error information)             |
      +------------+--------------------------------------------------------------------------------------------------------------------------+
      | MRS.300    | MRS system error. Try again later or contact customer service.                                                           |
      +------------+--------------------------------------------------------------------------------------------------------------------------+

-  For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
