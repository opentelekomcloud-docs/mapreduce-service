:original_name: mrs_02_1096.html

.. _mrs_02_1096:

Querying Monitoring Data
========================

Function
--------

This API is used to query performance monitoring items supported by a specified host.

URI
---

-  Format

GET /web/v1/monitor/metrics_info

-  Parameter description

+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter             | Mandatory or Not      | Description                                                                                                                                                             |
+=======================+=======================+=========================================================================================================================================================================+
| metric_names          | Yes                   | Monitoring metric name. Use commas (,) to separate metric names. You can enter a maximum of 10 metric names at a time.                                                  |
|                       |                       |                                                                                                                                                                         |
|                       |                       | Example metric names are as follows:                                                                                                                                    |
|                       |                       |                                                                                                                                                                         |
|                       |                       | -  **hm_cpu_used**: CPU usage                                                                                                                                           |
|                       |                       | -  **hm_cpu_core_num**: Number of CPU cores                                                                                                                             |
+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| metric_period         | No                    | Metric period, which can be real time, 5 minutes, 30 minutes, or 60 minutes                                                                                             |
+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| start_time            | No                    | Start time, expressed in milliseconds. The data type is Long. The default value is the earliest system time.                                                            |
+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| end_time              | No                    | End time, expressed in milliseconds. The data type is Long. The default value is the latest system time.                                                                |
+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| hosts                 | No                    | List of host names to be queried. Use commas (,) to separate host names. You can enter a maximum of 50 host names to meet the input length requirements of the browser. |
+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| host_group            | No                    | Name of the host group created by a user. This function is not available in the current version.                                                                        |
+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| metric_node_type      | No                    | You can set this parameter to obtain the monitoring metrics of a node. The possible values are as follows:                                                              |
|                       |                       |                                                                                                                                                                         |
|                       |                       | -  **active**: Indicates that you can obtain monitoring metrics of the active node.                                                                                     |
|                       |                       | -  **standby**: Indicates that you can obtain monitoring metrics of the standby node.                                                                                   |
|                       |                       | -  **all**: Indicates that you can obtain monitoring metrics of all nodes.                                                                                              |
+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| extend                | No                    | Metric extended field, which records information about small metrics                                                                                                    |
+-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

-  Example:

   .. code-block:: text

      GET /web/v1/monitor/metrics_info?metric_names=null&metric_period=null&start_time=null&end_time=null&hosts=null&host_group=null&metric_node_type=null&extend=null HTTP/1.1
      Host: example.com
      Content-Type: application/json
      Accept:application/json

-  Parameter description

   None

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
     "total_progress": 0,
     "res_obj": {
       "metric_datas": {
         "additionalProp1": [
           {
             "time": 0,
             "value": "string",
             "node": "string"
           }
         ]
       }
     }
   }

-  Request parameter description

.. table:: **Table 1** Response parameter description

   +-------------------+------------------+-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter         | Mandatory or Not | Type      | Description                                                                                                                                                       |
   +===================+==================+===========+===================================================================================================================================================================+
   | id                | No               | LONG      | Asynchronous task ID (meaningless in other scenarios). The default value is **-1**.                                                                               |
   +-------------------+------------------+-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | state             | No               | STRING    | Cluster status. The value **FAILED** indicates that the command fails to be executed. The value **COMPLETE** indicates that the command is successfully executed. |
   +-------------------+------------------+-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | error_code        | No               | INTEGER   | Error code returned                                                                                                                                               |
   +-------------------+------------------+-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | error_description | No               | STRING    | Error code description                                                                                                                                            |
   +-------------------+------------------+-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | total_progress    | No               | FLOAT     | Total progress                                                                                                                                                    |
   +-------------------+------------------+-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | res_obj           | No               | REFERENCE | Response object                                                                                                                                                   |
   +-------------------+------------------+-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 2** **res_obj** parameter description

   +-----------------+------------------+-----------------+----------------------------------------------------------------+
   | Parameter       | Mandatory or Not | Type            | Description                                                    |
   +=================+==================+=================+================================================================+
   | metric_datas    | No               | MAP             | Monitoring data.                                               |
   |                 |                  |                 |                                                                |
   |                 |                  |                 | Key indicates the name of a monitoring item.                   |
   |                 |                  |                 |                                                                |
   |                 |                  |                 | Value indicates a list of monitored metric parameters queried. |
   +-----------------+------------------+-----------------+----------------------------------------------------------------+

.. table:: **Table 3** **metricDataBean** parameter description

   +-----------+------------------+------------+----------------------------------------------------------------------+
   | Parameter | Mandatory or Not | Type       | Description                                                          |
   +===========+==================+============+======================================================================+
   | time      | No               | BIGDECIMAL | Time when monitoring metric value is collected                       |
   +-----------+------------------+------------+----------------------------------------------------------------------+
   | value     | No               | STRING     | Monitoring metric value                                              |
   +-----------+------------------+------------+----------------------------------------------------------------------+
   | node      | No               | STRING     | Node where the monitoring metric is collected                        |
   +-----------+------------------+------------+----------------------------------------------------------------------+
   | extend    | No               | STRING     | Metric extended field, which records information about small metrics |
   +-----------+------------------+------------+----------------------------------------------------------------------+

Status Code
-----------

=========== ============================
Status Code Description
=========== ============================
200         The operation is successful.
=========== ============================

For details about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
