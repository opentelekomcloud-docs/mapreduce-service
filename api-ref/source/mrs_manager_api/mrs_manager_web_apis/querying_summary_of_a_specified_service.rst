:original_name: mrs_02_1097.html

.. _mrs_02_1097:

Querying Summary of a Specified Service
=======================================

Function
--------

This API is used to query summary of a specified service in a cluster.

URI
---

-  Format

GET /web/v1/cluster/{cluster_id}/services/{service_name}

-  URI parameter description

+-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter             | Mandatory or Not      | Description                                                                                                                                          |
+=======================+=======================+======================================================================================================================================================+
| cluster_id            | Yes                   | Cluster ID that is displayed on MRS Manager. The default cluster ID is **1**, because MRS Manager supports management of only one cluster currently. |
+-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
| service_name          | Yes                   | Name of the service to be queried.                                                                                                                   |
|                       |                       |                                                                                                                                                      |
|                       |                       | For example, the service name is HBase, HDFS, or Spark.                                                                                              |
+-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

-  Example:

   .. code-block:: text

      GET /web/v1/cluster/{cluster_id}/services/{service_name} HTTP/1.1
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
      Content-Type: application/json  {
        "id": 0,
        "state": "NEW",
        "error_code": 0,
        "error_description": "string",
        "total_progress": 0,
        "res_obj": {
          "key_property": [
            {
              "name": "string",
              "value": {},
              "type": "TEXT"
            }
          ]
        }
      }

-  Parameter description

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

      +-----------------+------------------+-----------------+----------------------+
      | Parameter       | Mandatory or Not | Type            | Description          |
      +=================+==================+=================+======================+
      | name            | No               | STRING          | Property name        |
      +-----------------+------------------+-----------------+----------------------+
      | value           | No               | <T>             | Property value       |
      +-----------------+------------------+-----------------+----------------------+
      | type            | No               | ENUM            | Property type        |
      |                 |                  |                 |                      |
      |                 |                  | <Enumeration>   | Possible values are: |
      |                 |                  |                 |                      |
      |                 |                  |                 | **STATUS**           |
      |                 |                  |                 |                      |
      |                 |                  |                 | **TEXT**             |
      +-----------------+------------------+-----------------+----------------------+

Status Code
-----------

=========== ============================
Status Code Description
=========== ============================
200         The operation is successful.
=========== ============================

For details about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
