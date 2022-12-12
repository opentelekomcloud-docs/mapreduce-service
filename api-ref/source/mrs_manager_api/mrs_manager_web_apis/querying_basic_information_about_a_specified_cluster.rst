:original_name: mrs_02_1090.html

.. _mrs_02_1090:

Querying Basic Information About a Specified Cluster
====================================================

Function
--------

This API is used to query basic information about a specified cluster.

URI
---

GET /web/v1/clusters

Request
-------

-  Example:

   .. code-block:: text

      GET /web/v1/clusters HTTP/1.1
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
          "clusters": [
            {
              "stack": "string",
              "id": 0,
              "name": "string",
              "description": "string",
              "version": "string",
              "cluster_state": "string",
              "stack_model": "string",
              "lic_state": "string"
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

   +-----------+------------------+-----------------+-------------------------------------------+
   | Parameter | Mandatory or Not | Type            | Description                               |
   +===========+==================+=================+===========================================+
   | clusters  | No               | ARRAY_REFERENCE | Records all installed clusters in arrays. |
   +-----------+------------------+-----------------+-------------------------------------------+

.. table:: **Table 3** **clusters** parameter description

   +-----------------+------------------+-----------------+-------------------------------------------------------------+
   | Parameter       | Mandatory or Not | Type            | Description                                                 |
   +=================+==================+=================+=============================================================+
   | stack           | No               | STRING          | Cluster version information                                 |
   +-----------------+------------------+-----------------+-------------------------------------------------------------+
   | id              | No               | INTEGER         | Cluster ID                                                  |
   +-----------------+------------------+-----------------+-------------------------------------------------------------+
   | name            | No               | STRING          | Cluster name                                                |
   +-----------------+------------------+-----------------+-------------------------------------------------------------+
   | description     | No               | STRING          | Cluster description                                         |
   +-----------------+------------------+-----------------+-------------------------------------------------------------+
   | version         | No               | STRING          | Cluster version                                             |
   +-----------------+------------------+-----------------+-------------------------------------------------------------+
   | cluster_state   | No               | STRING          | Cluster status. Possible values are as follows:             |
   |                 |                  |                 |                                                             |
   |                 |                  |                 | **Null**: There is no special status.                       |
   |                 |                  |                 |                                                             |
   |                 |                  |                 | **installingPatch**: The patch is being installed.          |
   +-----------------+------------------+-----------------+-------------------------------------------------------------+
   | stack_model     | No               | STRING          | Security mode of a cluster. Possible values are as follows: |
   |                 |                  |                 |                                                             |
   |                 |                  |                 | NoSec: Normal mode                                          |
   |                 |                  |                 |                                                             |
   |                 |                  |                 | Sec: Security mode                                          |
   +-----------------+------------------+-----------------+-------------------------------------------------------------+
   | lic_state       | No               | STRING          | License status                                              |
   +-----------------+------------------+-----------------+-------------------------------------------------------------+

Status Code
-----------

=========== ============================
Status Code Description
=========== ============================
200         The operation is successful.
=========== ============================

For details about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
