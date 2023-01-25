:original_name: mrs_02_0044.html

.. _mrs_02_0044:

Querying the Job Object List
============================

Function
--------

This API is used to query the job object list. This API is compatible with Sahara.

URI
---

-  Format

   GET /v1.1/{project_id}/jobs

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
      | Parameter             | Mandatory             | Description                                                                                               |
      +=======================+=======================+===========================================================================================================+
      | project_id            | Yes                   | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
      | limit                 | No                    | Maximum number of objects in response data                                                                |
      |                       |                       |                                                                                                           |
      |                       |                       | Value range: 1 to 1073741822                                                                              |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
      | marker                | No                    | The ID is the ID of the last element in the list that will not be returned.                               |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
      | sort_by               | No                    | Sort field. A hyphen (-) before the sort field indicates to sort in descending order. Examples:           |
      |                       |                       |                                                                                                           |
      |                       |                       | -  **sort_by=name** indicates to sort by **name** in ascending order.                                     |
      |                       |                       | -  **sort_by=-name** indicates to sort by name in descending order.                                       |
      +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

None

Response
--------

.. table:: **Table 2** Response parameter description

   +-----------------------+-----------------------+---------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                         |
   +=======================+=======================+=====================================================================+
   | markers               | Object                | Markers object                                                      |
   |                       |                       |                                                                     |
   |                       |                       | For details, see :ref:`Table 3 <mrs_02_0044__table35904709104244>`. |
   +-----------------------+-----------------------+---------------------------------------------------------------------+
   | jobs                  | Array                 | Job object list                                                     |
   |                       |                       |                                                                     |
   |                       |                       | For details, see :ref:`Table 4 <mrs_02_0044__table5154210817547>`.  |
   +-----------------------+-----------------------+---------------------------------------------------------------------+

.. _mrs_02_0044__table35904709104244:

.. table:: **Table 3** **markers** parameter description

   ========= ====== ===========================
   Parameter Type   Description
   ========= ====== ===========================
   prev      String Marker on the previous page
   next      String Marker on the next page
   ========= ====== ===========================

.. _mrs_02_0044__table5154210817547:

.. table:: **Table 4** **jobs** parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                               |
   +=======================+=======================+===========================================================================================================+
   | description           | String                | Job object description                                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | tenant_id             | String                | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | created_at            | String                | Job object creation time                                                                                  |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | mains                 | Array                 | Executable program set of a job object                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | updated_at            | String                | Job object update time                                                                                    |
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

   .. code-block:: text

      GET /v1.1/{project_id}/jobs?limit=2&sort_by=name&marker=4f59aa66-bf38-402c-9b6f-320e77219b9b

-  Example response

   .. code-block::

      {
          "markers": {
              "prev": "62a287e9-76c3-458d-a2f8-56e2d824a9ee",
              "next": null
          },
          "jobs": [
              {
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
              },
              {
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
          ]
      }

Status Code
-----------

:ref:`Table 5 <mrs_02_0044__table1584477916050>` describes the status code of this API.

.. _mrs_02_0044__table1584477916050:

.. table:: **Table 5** Status code

   =========== ============================================
   Status code Description
   =========== ============================================
   200         The job object list is queried successfully.
   =========== ============================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
