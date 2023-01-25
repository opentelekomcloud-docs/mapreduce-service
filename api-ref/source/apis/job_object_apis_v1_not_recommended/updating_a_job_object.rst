:original_name: mrs_02_0042.html

.. _mrs_02_0042:

Updating a Job Object
=====================

Function
--------

This API is used to update a job object. This API is compatible with Sahara.

URI
---

-  Format

   PATCH /v1.1/{project_id}/jobs/{job_id}

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Parameter  | Mandatory | Description                                                                                               |
      +============+===========+===========================================================================================================+
      | project_id | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | job_id     | Yes       | Job object ID                                                                                             |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------+

Request
-------

.. table:: **Table 2** Request parameter description

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                         |
   +=================+=================+=================+=====================================================================================================+
   | name            | No              | String          | Job object name                                                                                     |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | Contains 1 to 64 characters and consists of letters, digits, hyphens (-), and underscores (_) only. |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | mains           | No              | Array           | Executable program set of a job object                                                              |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | The current version does not support update of the executable program set.                          |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | libs            | No              | Array           | Dependency package set of a job object                                                              |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | The current version does not support update of the dependency package set.                          |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | is_protected    | No              | Bool            | Whether a job object is protected                                                                   |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | -  true                                                                                             |
   |                 |                 |                 | -  false                                                                                            |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | The current version does not support this function.                                                 |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | interface       | No              | Array           | User-defined interface set                                                                          |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | The current version does not support this function.                                                 |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | is_public       | No              | Bool            | Whether a job object is public                                                                      |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | -  true                                                                                             |
   |                 |                 |                 | -  false                                                                                            |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | The current version does not support this function.                                                 |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | type            | No              | String          | Job object type                                                                                     |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | -  MapReduce                                                                                        |
   |                 |                 |                 | -  Spark                                                                                            |
   |                 |                 |                 | -  Hive                                                                                             |
   |                 |                 |                 | -  DistCp                                                                                           |
   |                 |                 |                 | -  SparkScript                                                                                      |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | description     | No              | String          | Job object description                                                                              |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | Contains a maximum of 65535 characters.                                                             |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+

Response
--------

.. table:: **Table 3** Response parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                               |
   +=======================+=======================+===========================================================================================================+
   | description           | String                | Job object description                                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | tenant_id             | String                | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | created_at            | String                | Job object creation time                                                                                  |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | updated_at            | String                | Job object update time                                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | mains                 | Array                 | Executable program set of a job object                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | libs                  | Array                 | Dependency package set of a job object                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_protected          | Bool                  | Whether a job object is protected                                                                         |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | interface             | Array                 | User-defined interface set                                                                                |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_public             | Bool                  | Whether a job object is public                                                                            |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | type                  | String                | Job object type                                                                                           |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | id                    | String                | Job object ID                                                                                             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | name                  | String                | Job object name                                                                                           |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   .. code-block::

      {
          "name": "my-mapreduce-job-update",
          "mains": [ ],
          "libs": [
          "2628d0e4-6109-4a09-a338-c4ee1b0963ed"
          ],
          "is_protected": false,
          "interface": [ ],
          "is_public": false,
          "type": "MapReduce",
          "description": "This is the Map Reduce job template"
      }

-  Example response

   .. code-block::

      {
          "job": {
              "name": "my-mapreduce-job-update",
              "type": "MapReduce",
              "description": "This is the Map Reduce job template",
              "mains": [],
              "libs": [
                  {
                      "name": "my-job-binary-666",
                      "url": "/simple/mapreduce/program",
                      "description": "this is the job binary template",
                      "id": "2628d0e4-6109-4a09-a338-c4ee1b0963ed",
                      "tenant_id": "5a3314075bfa49b9ae360f4ecd333695",
                      "is_public": false,
                      "is_protected": false,
                      "extra": null
                  }
              ],
              "created_at": "2017-06-22T12:05:58",
              "updated_at": "2017-06-22T12:05:58",
              "id": "b8ea4daa-0042-45e0-a522-e8b714e74760",
              "tenant_id": "5a3314075bfa49b9ae360f4ecd333695",
              "is_public": false,
              "is_protected": false,
              "interface": []
          }
      }

Status Code
-----------

:ref:`Table 4 <mrs_02_0042__table1584477916050>` describes the status code of this API.

.. _mrs_02_0042__table1584477916050:

.. table:: **Table 4** Status code

   =========== =============================================
   Status code Description
   =========== =============================================
   202         The job object has been successfully updated.
   =========== =============================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
