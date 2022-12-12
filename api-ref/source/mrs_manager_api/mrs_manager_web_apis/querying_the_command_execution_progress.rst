:original_name: mrs_02_1091.html

.. _mrs_02_1091:

Querying the Command Execution Progress
=======================================

Function
--------

This API is used to query the command execution progress by command ID, including the total progress and the detailed progress of each step.

URI
---

-  Format

GET /web/v1/common/command/{command_id}/progress

-  URI parameter description

+-----------------------+-----------------------+------------------------------------------------------------------------------------------------------+
| Parameter             | Mandatory or Not      | Description                                                                                          |
+=======================+=======================+======================================================================================================+
| command_id            | Yes                   | Command ID, which can be obtained from the response of the asynchronous request                      |
|                       |                       |                                                                                                      |
|                       |                       | Asynchronous requests include requests for saving configurations and starting and stopping services. |
+-----------------------+-----------------------+------------------------------------------------------------------------------------------------------+

Request
-------

-  Example:

   .. code-block:: text

      GET /web/v1/common/command/{command_id}/progress HTTP/1.1
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
          "cluster_id": 0,
          "step_list": [
            {
              "name": "string",
              "description": "string"
            }
          ],
          "fail_entity_list": [
            {
              "fail_entity": "string",
              "operation_type": "string"
            }
          ],
          "total_step_size": 0
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

   +------------------+------------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Mandatory or Not | Type            | Description                                                                                                                                                                           |
   +==================+==================+=================+=======================================================================================================================================================================================+
   | cluster_id       | No               | INTEGER         | Cluster ID                                                                                                                                                                            |
   +------------------+------------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | step_list        | Yes              | ARRAY_REFERENCE | Records the progress of each step in an array. A command may be divided into multiple steps for execution.                                                                            |
   +------------------+------------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | fail_entity_list | No               | ARRAY_REFERENCE | List of failed operations. Currently, this function is supported for starting, stopping, and restarting the service. Other operations are not supported (an empty array is returned). |
   +------------------+------------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | total_step_size  | Yes              | INTEGER         | Total command execution progress. The value ranges from 0 to 100.                                                                                                                     |
   +------------------+------------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** **step_list** parameter description

   =========== ================ ====== ==============
   Parameter   Mandatory or Not Type   Description
   =========== ================ ====== ==============
   name        No               STRING Partition name
   description No               STRING Description
   =========== ================ ====== ==============

.. table:: **Table 4** **fail_entity_list** parameter description

   ============== ================ ====== =============================
   Parameter      Mandatory or Not Type   Description
   ============== ================ ====== =============================
   fail_entity    No               STRING Failed instance
   operation_type No               STRING Operation type: STOP or START
   ============== ================ ====== =============================

Status Code
-----------

=========== ============================
Status Code Description
=========== ============================
200         The operation is successful.
=========== ============================

For details about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
