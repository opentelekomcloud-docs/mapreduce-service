:original_name: mrs_02_0037.html

.. _mrs_02_0037:

Querying the Binary Object Details
==================================

Function
--------

This API is used to query detailed information about a binary object. This API is compatible with Sahara.

URI
---

-  Format

   GET /v1.1/{project_id}/job-binaries/{job_binary_id}

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +---------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Parameter     | Mandatory | Description                                                                                               |
      +===============+===========+===========================================================================================================+
      | project_id    | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +---------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | job_binary_id | Yes       | Binary object ID                                                                                          |
      +---------------+-----------+-----------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

None

Response
--------

.. table:: **Table 2** Response parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                               |
   +=======================+=======================+===========================================================================================================+
   | is_public             | Bool                  | Whether a binary object is public                                                                         |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | description           | String                | Binary object description                                                                                 |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | url                   | String                | Binary object URL                                                                                         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | tenant_id             | String                | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | created_at            | String                | Binary object creation time                                                                               |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | updated_at            | String                | Binary object update time                                                                                 |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | id                    | String                | Binary object ID                                                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | name                  | String                | Binary object name                                                                                        |
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

   None

-  Example response

   .. code-block::

      {
          "job_binary": {
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
      }

Status Code
-----------

:ref:`Table 3 <mrs_02_0037__table1584477916050>` describes the status code of this API.

.. _mrs_02_0037__table1584477916050:

.. table:: **Table 3** Status code

   =========== ===================================================
   Status code Description
   =========== ===================================================
   200         The binary object details are queried successfully.
   =========== ===================================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
