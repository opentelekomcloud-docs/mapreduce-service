:original_name: mrs_02_0045.html

.. _mrs_02_0045:

Querying Job Object Details
===========================

Function
--------

This API is used to query detailed information about a job object. This API is compatible with Sahara.

URI
---

-  Format

   GET /v1.1/{project_id}/jobs/{job_id}

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

**Request parameters**

None

Response
--------

.. table:: **Table 2** Response parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                               |
   +=======================+=======================+===========================================================================================================+
   | tenant_id             | String                | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | created_at            | String                | Job object creation time                                                                                  |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | id                    | String                | Job object ID                                                                                             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | name                  | String                | Job object name                                                                                           |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | updated_at            | String                | Job object update time                                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | description           | String                | Job object description                                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | interface             | Array                 | User-defined interface set                                                                                |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | libs                  | Array                 | Dependency package set of a job object                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | type                  | String                | Job object type                                                                                           |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | mains                 | Array                 | Executable program set of a job object                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_protected          | Bool                  | Whether a job object is protected                                                                         |
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
          "job": {
              "name": "my-mapreduce-job",
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
              "created_at": "2017-06-22T09:39:13",
              "updated_at": "2017-06-22T09:39:13",
              "id": "38a04cba-c113-4868-b11f-f50e8b1bf252",
              "tenant_id": "5a3314075bfa49b9ae360f4ecd333695",
              "is_public": false,
              "is_protected": false,
              "interface": []
          }
      }

Status Code
-----------

:ref:`Table 3 <mrs_02_0045__table1584477916050>` describes the status code of this API.

.. _mrs_02_0045__table1584477916050:

.. table:: **Table 3** Status code

   =========== ================================================
   Status code Description
   =========== ================================================
   200         The job object details are queried successfully.
   =========== ================================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
