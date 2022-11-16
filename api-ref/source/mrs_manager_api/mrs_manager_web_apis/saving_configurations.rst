:original_name: mrs_02_1092.html

.. _mrs_02_1092:

Saving Configurations
=====================

Function
--------

This API is used to save configurations of services, roles, and instances. This API allows you to perform the following operations:

-  Modify multiple configuration items at a time.

-  Modify multiple configuration items at service, role, and instance levels at a time.

URI
---

-  Format

POST /web/v1/config/cluster/{cluster_id}/save

-  Parameter description

+------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter  | Mandatory or Not | Description                                                                                                                                          |
+============+==================+======================================================================================================================================================+
| cluster_id | Yes              | Cluster ID that is displayed on MRS Manager. The default cluster ID is **1**, because MRS Manager supports management of only one cluster currently. |
+------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

-  Example:

.. code-block:: text

   POST /web/v1/config/cluster/{cluster_id}/save HTTP/1.1
   Host: example.com
   Content-Type: application/json
   Accept:application/json
   {
     "id": 0,
     "user_password": "string",
     "configurations_summary": {
       "restart_affected_components": true,
       "components": [
         {
           "component_name": "string",
           "configurations": [
             {
               "name": "string",
               "value": "string",
               "default_value": "string",
               "description": "string",
               "type": "string",
               "config_group_type": "string",
               "config_group": "string",
               "item_type": "string",
               "item_conf": "string",
               "item_event": "string",
               "weak_reference": "string"
             }
           ],
           "children": [
             {
               "role_name": "string",
               "configurations": [],
               "children": [
                 {
                   "node": {
                     "id": 0,
                     "name": "string",
                     "description": "string",
                     "controller_id": "string",
                     "ip_address": "string",
                     "business_ip_address": "string",
                     "rack": "string",
                     "host_name": "string",
                     "total_memory": "string",
                     "available_memory": "string",
                     "total_hard_disk_space": "string",
                     "available_hard_disk_space": "string",
                     "no_of_CPUs": "string",
                     "available_swap_memory": "string",
                     "total_swap_memory": "string",
                     "cpu_usage": "string",
                     "disk_usage": "string",
                     "health_status": "GOOD",
                     "memory_usage": "string",
                     "swap_memory_usage": "string",
                     "files_info": [
                       {
                         "name": "string",
                         "description": "string"
                       }
                     ],
                     "operational_status": "STARTED",
                     "network_read": "string",
                     "network_write": "string",
                     "instances": [
                       {
                         "name": "string",
                         "id": "string",
                         "operational_status": "STARTED",
                         "health_status": "GOOD",
                         "ha_status": "ACTIVE",
                         "config_status": {
                           "level": "string",
                           "status": "UNKNOWN",
                           "description": "string"
                         },
                         "role_name": "string",
                         "service_name": "string",
                         "web_UI_address": "string",
                         "is_service_role": true,
                         "pair_name": "string",
                         "support_decom": true
                       }
                     ],
                     "is_OMS_node": true
                   },
                   "configurations": []
                 }
               ],
               "classification": [
                 {
                   "name": "string",
                   "description": "string"
                 }
               ]
             }
           ],
           "classification": [
             {
               "name": "string",
               "description": "string"
             }
           ]
         }
       ]
     }
   }

-  Parameter description

.. table:: **Table 1** Request parameter description

   +------------------------+------------------+-----------+-------------------------------------------------------------------------------------+
   | Parameter              | Mandatory or Not | Type      | Description                                                                         |
   +========================+==================+===========+=====================================================================================+
   | id                     | No               | LONG      | Asynchronous task ID (meaningless in other scenarios). The default value is **-1**. |
   +------------------------+------------------+-----------+-------------------------------------------------------------------------------------+
   | user_password          | No               | STRING    | User password                                                                       |
   +------------------------+------------------+-----------+-------------------------------------------------------------------------------------+
   | configurations_summary | Yes              | REFERENCE | Configures a description object.                                                    |
   +------------------------+------------------+-----------+-------------------------------------------------------------------------------------+

.. table:: **Table 2** **configurations_summary** parameter description

   +-----------------------------+------------------+-----------------+--------------------------------------------+
   | Parameter                   | Mandatory or Not | Type            | Description                                |
   +=============================+==================+=================+============================================+
   | restart_affected_components | No               | BOOLEAN         | Whether to restart the affected components |
   |                             |                  |                 |                                            |
   |                             |                  |                 | **true**: Restart                          |
   |                             |                  |                 |                                            |
   |                             |                  |                 | **false**: Do not restart                  |
   +-----------------------------+------------------+-----------------+--------------------------------------------+
   | components                  | No               | ARRAY_REFERENCE | Service list                               |
   +-----------------------------+------------------+-----------------+--------------------------------------------+

.. table:: **Table 3** **components** parameter description

   +----------------+------------------+-----------------+------------------------------------------------------------------------+
   | Parameter      | Mandatory or Not | Type            | Description                                                            |
   +================+==================+=================+========================================================================+
   | component_name | No               | STRING          | Service name                                                           |
   +----------------+------------------+-----------------+------------------------------------------------------------------------+
   | configurations | No               | ARRAY_REFERENCE | Description of the service, role, or instance level.                   |
   +----------------+------------------+-----------------+------------------------------------------------------------------------+
   | children       | No               | ARRAY_REFERENCE | Sublevel description array. The sublevel of the service level is role. |
   +----------------+------------------+-----------------+------------------------------------------------------------------------+
   | classification | No               | ARRAY_REFERENCE | Configuration definition information                                   |
   +----------------+------------------+-----------------+------------------------------------------------------------------------+

.. table:: **Table 4** **children** parameter description

   +----------------+------------------+-----------------+-------------------------------------------------------------------------------+
   | Parameter      | Mandatory or Not | Type            | Description                                                                   |
   +================+==================+=================+===============================================================================+
   | role_name      | No               | STRING          | Role name                                                                     |
   +----------------+------------------+-----------------+-------------------------------------------------------------------------------+
   | configurations | No               | ARRAY_REFERENCE | Configuration item description array: Service level/role level/instance level |
   +----------------+------------------+-----------------+-------------------------------------------------------------------------------+
   | children       | No               | ARRAY_REFERENCE | Sublevel description array. The sublevel of the role level is instance.       |
   +----------------+------------------+-----------------+-------------------------------------------------------------------------------+
   | classification | No               | ARRAY_REFERENCE | Configuration definition information                                          |
   +----------------+------------------+-----------------+-------------------------------------------------------------------------------+

.. table:: **Table 5** **configurations** parameter description of services, roles, and instances

   +-------------------+------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter         | Mandatory or Not | Type   | Description                                                                                                                                                                                                                                             |
   +===================+==================+========+=========================================================================================================================================================================================================================================================+
   | name              | No               | STRING | Name of the configuration item to be saved                                                                                                                                                                                                              |
   +-------------------+------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | value             | No               | STRING | Value to be saved                                                                                                                                                                                                                                       |
   +-------------------+------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | default_value     | No               | STRING | Default value                                                                                                                                                                                                                                           |
   +-------------------+------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | description       | No               | STRING | Configuration item description                                                                                                                                                                                                                          |
   +-------------------+------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | type              | No               | STRING | Configuration item type                                                                                                                                                                                                                                 |
   +-------------------+------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | config_group_type | No               | STRING | Configuration group type                                                                                                                                                                                                                                |
   +-------------------+------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | config_group      | No               | STRING | Configuration group                                                                                                                                                                                                                                     |
   +-------------------+------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | item_type         | No               | STRING | Type of the configuration item value to be saved                                                                                                                                                                                                        |
   +-------------------+------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | item_conf         | No               | STRING | Configuration item value validity check                                                                                                                                                                                                                 |
   +-------------------+------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | item_event        | No               | STRING | Event type of a configuration item. Currently, only **hide-show** is supported.                                                                                                                                                                         |
   +-------------------+------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | weak_reference    | No               | STRING | Whether a configuration item is a weak reference. If the configuration item is a weak reference, the configuration parsing is passed even though the configuration item name or role name does not exist, and the value will be set to an empty string. |
   +-------------------+------------------+--------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 6** **classification** parameter description

   =========== ================ ====== ===========
   Parameter   Mandatory or Not Type   Description
   =========== ================ ====== ===========
   name        No               STRING Name
   description No               STRING Description
   =========== ================ ====== ===========

Response
--------

-  Example:

   .. code-block::

      HTTP/1.1 200 OK
      Data:Wed,02 May 2018 10:10:01 GMT
      Server: example-server
      Content-Type: application/json
      {
        "id": 0,
        "state": "COMPLETE",
        "error_code": 0,
        "error_description": "string",
        "total_progress": 0
      }

-  Response parameter description

+-------------------+------------------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter         | Mandatory or Not | Type    | Description                                                                                                                                                       |
+===================+==================+=========+===================================================================================================================================================================+
| id                | No               | LONG    | Asynchronous task ID (meaningless in other scenarios). The default value is **-1**.                                                                               |
+-------------------+------------------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| state             | No               | STRING  | Cluster status. The value **FAILED** indicates that the command fails to be executed. The value **COMPLETE** indicates that the command is successfully executed. |
+-------------------+------------------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| error_code        | No               | INTEGER | Error code returned                                                                                                                                               |
+-------------------+------------------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| error_description | No               | STRING  | Error code description                                                                                                                                            |
+-------------------+------------------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| total_progress    | No               | FLOAT   | Total progress                                                                                                                                                    |
+-------------------+------------------+---------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Status Code
-----------

=========== ============================
Status Code Description
=========== ============================
200         The operation is successful.
=========== ============================

For details about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
