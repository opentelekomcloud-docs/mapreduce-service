:original_name: mrs_02_0034.html

.. _mrs_02_0034:

Creating a Job Binary Object
============================

Function
--------

This API is used to create a job binary object. This API is compatible with Sahara.

URI
---

-  Format

   POST /v1.1/{project_id}/job-binaries

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Parameter  | Mandatory | Description                                                                                               |
      +============+===========+===========================================================================================================+
      | project_id | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------+

Request
-------

.. table:: **Table 2** Request parameter description

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                         |
   +=================+=================+=================+=====================================================================================================+
   | name            | Yes             | String          | Binary object name                                                                                  |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | Contains 1 to 80 characters and consists of letters, digits, hyphens (-), and underscores (_) only. |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | url             | Yes             | String          | Binary object URL, which contains of 1 to 255 characters.                                           |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | The URL must start with **s3a://** or **/**.                                                        |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | is_protected    | No              | Bool            | Whether a binary object is protected                                                                |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | -  true                                                                                             |
   |                 |                 |                 | -  false                                                                                            |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | The current version does not support this function.                                                 |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | is_public       | No              | Bool            | Whether a binary object is public                                                                   |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | -  true                                                                                             |
   |                 |                 |                 | -  false                                                                                            |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | The current version does not support this function.                                                 |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | description     | Yes             | String          | Binary object description                                                                           |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | Contains a maximum of 65535 characters.                                                             |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+

Response
--------

.. table:: **Table 3** Response parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                               |
   +=======================+=======================+===========================================================================================================+
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
   | is_protected          | Bool                  | Whether a binary object is protected                                                                      |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_public             | Bool                  | Whether a binary object is public                                                                         |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | id                    | String                | Binary object ID                                                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | name                  | String                | Binary object name                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   .. code-block::

      {
          "name": "my-job-binary",
          "url": "/simple/mapreduce/program",
          "is_protected": false,
          "is_public": false,
          "description": "this is the job binary template"
      }

-  Example response

   .. code-block::

      {
          "job_binary": {
              "name": "my-job-binary",
              "url": "/simple/mapreduce/program",
              "description": "this is the job binary template",
              "created_at": "2017-06-22T09:04:53",
              "updated_at": null,
              "id": "da37b581-042f-4d7a-9378-f628f32bd9ae",
              "tenant_id": "5a3314075bfa49b9ae360f4ecd333695",
              "is_public": false,
              "is_protected": false
          }
      }

Status Code
-----------

:ref:`Table 4 <mrs_02_0034__table1584477916050>` describes the status code of this API.

.. _mrs_02_0034__table1584477916050:

.. table:: **Table 4** Status code

   =========== ====================================================
   Status Code Description
   =========== ====================================================
   202         The job binary object has been successfully created.
   =========== ====================================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
