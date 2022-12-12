:original_name: mrs_02_1089.html

.. _mrs_02_1089:

Querying the Health Status of a Specified Cluster
=================================================

Function
--------

This API is used to query the health status of a specified cluster. If any component is unavailable, the abnormal cluster health status is returned.

URI
---

-  Format

GET /web/v1/cluster/{cluster_id}/status

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

      GET /web/v1/cluster/{cluster_id}/status HTTP/1.1
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
          "state": "GOOD"
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

   +-----------------+------------------+-----------------+------------------------------------+
   | Parameter       | Mandatory or Not | Type            | Description                        |
   +=================+==================+=================+====================================+
   | state           | Yes              | STRING          | Cluster health status              |
   |                 |                  |                 |                                    |
   |                 |                  |                 | **Good**: The cluster is healthy.  |
   |                 |                  |                 |                                    |
   |                 |                  |                 | **Bad**: The cluster is unhealthy. |
   +-----------------+------------------+-----------------+------------------------------------+

Status Code
-----------

=========== ============================
Status Code Description
=========== ============================
200         The operation is successful.
=========== ============================

For details about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
