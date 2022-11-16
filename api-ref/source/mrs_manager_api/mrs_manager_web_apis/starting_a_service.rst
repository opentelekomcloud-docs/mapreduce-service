:original_name: mrs_02_1094.html

.. _mrs_02_1094:

Starting a Service
==================

Function
--------

This API is used to start a specified service.

URI
---

-  Format

POST /web/v1/maintain/cluster/{cluster_id}/service/{service_name}/start

-  URI parameter description

+--------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter    | Mandatory or Not | Description                                                                                                                                          |
+==============+==================+======================================================================================================================================================+
| service_name | Yes              | Name of the service to be started                                                                                                                    |
+--------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+
| cluster_id   | Yes              | Cluster ID that is displayed on MRS Manager. The default cluster ID is **1**, because MRS Manager supports management of only one cluster currently. |
+--------------+------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

-  Example:

   .. code-block:: text

      POST /web/v1/maintain/cluster/{cluster_id}/service/{service_name}/start HTTP/1.1
      Host: example.com
      Content-Type: application/json
      Accept:application/json
      {
        "user_password": "string",
        "only_self": true
      }

-  Parameter description

.. table:: **Table 1** Request parameter description

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory or Not      | Description                                                                                                                                                                            |
   +=======================+=======================+========================================================================================================================================================================================+
   | user_password         | No                    | Password of the login user. This parameter is used for secondary authentication. You do not need to enter a specific value when starting the service. The parameter value can be null. |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | only_self             | No                    | Whether to operate only the specified service                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                        |
   |                       |                       | **false**: The services on which the service depends are also started.                                                                                                                 |
   |                       |                       |                                                                                                                                                                                        |
   |                       |                       | **true**: Only the specified service is started.                                                                                                                                       |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

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

+-------------------+------------------+-----------------+-------------------------------------------------------------------------------------+
| Parameter         | Mandatory or Not | Type            | Description                                                                         |
+===================+==================+=================+=====================================================================================+
| id                | No               | LONG            | Asynchronous task ID (meaningless in other scenarios). The default value is **-1**. |
+-------------------+------------------+-----------------+-------------------------------------------------------------------------------------+
| state             | No               | STRING          | Cluster status                                                                      |
|                   |                  |                 |                                                                                     |
|                   |                  |                 | -  **FAILED**: The command failed to be executed.                                   |
|                   |                  |                 | -  **COMPLETE**: The command is executed successfully.                              |
|                   |                  |                 | -  IN_PROGRESS: The command is being executed.                                      |
+-------------------+------------------+-----------------+-------------------------------------------------------------------------------------+
| error_code        | No               | INTEGER         | Error code returned                                                                 |
+-------------------+------------------+-----------------+-------------------------------------------------------------------------------------+
| error_description | No               | STRING          | Error code description                                                              |
+-------------------+------------------+-----------------+-------------------------------------------------------------------------------------+
| total_progress    | No               | FLOAT           | Total progress                                                                      |
+-------------------+------------------+-----------------+-------------------------------------------------------------------------------------+

Status Code
-----------

=========== ============================
Status Code Description
=========== ============================
200         The operation is successful.
=========== ============================

For details about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
