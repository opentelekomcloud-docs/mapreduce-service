:original_name: mrs_02_0036.html

.. _mrs_02_0036:

Querying the Binary Object List
===============================

Function
--------

This API is used to query the binary object list. This API is compatible with Sahara.

URI
---

-  Format

   GET /v1.1/{project_id}/job-binaries

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Mandatory             | Description                                                                                                                                                      |
      +=======================+=======================+==================================================================================================================================================================+
      | project_id            | Yes                   | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`.                                                        |
      +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | limit                 | No                    | Maximum number of objects in response data                                                                                                                       |
      |                       |                       |                                                                                                                                                                  |
      |                       |                       | Value range: 1 to 1073741822                                                                                                                                     |
      +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | marker                | No                    | Job binary object ID                                                                                                                                             |
      |                       |                       |                                                                                                                                                                  |
      |                       |                       | Query the job binary object list, and select one job binary object ID as the marker. The ID is the ID of the last element in the list that will not be returned. |
      +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | sort_by               | No                    | Sort field                                                                                                                                                       |
      |                       |                       |                                                                                                                                                                  |
      |                       |                       | A hyphen (-) before the sort field indicates to sort in descending order. Example:                                                                               |
      |                       |                       |                                                                                                                                                                  |
      |                       |                       | -  **sort_by=name** indicates to sort by name in ascending order.                                                                                                |
      |                       |                       | -  **sort_by=-name** indicates to sort by name in descending order.                                                                                              |
      +-----------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

None.

Response
--------

.. table:: **Table 2** Response parameter description

   +-----------------------+-----------------------+---------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                         |
   +=======================+=======================+=====================================================================+
   | markers               | Object                | Markers object                                                      |
   |                       |                       |                                                                     |
   |                       |                       | For details, see :ref:`Table 3 <mrs_02_0036__table35904709104244>`. |
   +-----------------------+-----------------------+---------------------------------------------------------------------+
   | binaries              | Array                 | Binary object list                                                  |
   |                       |                       |                                                                     |
   |                       |                       | For details, see :ref:`Table 4 <mrs_02_0036__table5646270112712>`.  |
   +-----------------------+-----------------------+---------------------------------------------------------------------+

.. _mrs_02_0036__table35904709104244:

.. table:: **Table 3** **markers** parameter description

   ========= ====== ===========================
   Parameter Type   Description
   ========= ====== ===========================
   prev      String Marker on the previous page
   next      String Marker on the next page
   ========= ====== ===========================

.. _mrs_02_0036__table5646270112712:

.. table:: **Table 4** **binaries** parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                               |
   +=======================+=======================+===========================================================================================================+
   | name                  | String                | Binary object name                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | url                   | String                | Binary object URL                                                                                         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | description           | String                | Binary object description                                                                                 |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | created_at            | String                | Binary object creation time                                                                               |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | updated_at            | String                | Binary object update time                                                                                 |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | id                    | String                | Binary object ID                                                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | tenant_id             | String                | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_public             | Bool                  | Whether a binary object is public                                                                         |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_protected          | Bool                  | Whether a binary object is protected                                                                      |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   .. code-block:: text

      GET /v1.1/{project_id}/job-binaries?limit=1&sort_by=name&marker= eadfb8ec-760b-499f-b8df-00a6def854f8

-  Example response

   .. code-block::

      {
          "markers": {
              "prev": "ddf13f9d-93e8-4999-b860-0dc0c01c517d",
              "next": null
          },
          "binaries": [
              {
                  "name": "my-job-binary-update",
                  "url": "/simple/mapreduce/program",
                  "description": "this is the job binary template",
                  "created_at": "2017-06-22T09:04:53",
                  "updated_at": "2017-06-22T09:06:50",
                  "id": "da37b581-042f-4d7a-9378-f628f32bd9ae",
                  "tenant_id": "5a3314075bfa49b9ae360f4ecd333695",
                  "is_public": false,
                  "is_protected": false
              }
          ]
      }

Status Code
-----------

:ref:`Table 5 <mrs_02_0036__table1584477916050>` describes the status code of this API.

.. _mrs_02_0036__table1584477916050:

.. table:: **Table 5** Status code

   =========== ===============================================
   Status Code Description
   =========== ===============================================
   200         The binary object list is queried successfully.
   =========== ===============================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
