:original_name: mrs_02_0041.html

.. _mrs_02_0041:

Creating a Job Object
=====================

Function
--------

This API is used to create a job object. This API is compatible with Sahara.

URI
---

-  Format

   POST /v1.1/{project_id}/jobs

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

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                 |
   +=================+=================+=================+=============================================================================================================+
   | name            | Yes             | String          | Job object name                                                                                             |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | Contains 1 to 64 characters and consists of letters, digits, hyphens (-), and underscores (_) only.         |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+
   | mains           | No              | Array           | Executable program set of a job object                                                                      |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | If the job type is Hive or Spark Script, the value of **mains** must not be empty.                          |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | For details on how to obtain the executable program, see :ref:`Creating a Job Binary Object <mrs_02_0034>`. |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+
   | libs            | No              | Array           | Dependency package set of a job object                                                                      |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | If the job type is MapReduce or Spark, the value of **libs** must not be empty.                             |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | For details on how to obtain the dependency package, see :ref:`Creating a Job Binary Object <mrs_02_0034>`. |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+
   | is_protected    | No              | Bool            | Whether a job object is protected                                                                           |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | -  true                                                                                                     |
   |                 |                 |                 | -  false                                                                                                    |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | The current version does not support this function.                                                         |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+
   | interface       | No              | Array           | User-defined interface set                                                                                  |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | The current version does not support this function.                                                         |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+
   | is_public       | No              | Bool            | Whether a job object is public                                                                              |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | -  true                                                                                                     |
   |                 |                 |                 | -  false                                                                                                    |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | The current version does not support this function.                                                         |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+
   | type            | Yes             | String          | Job object type                                                                                             |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | -  MapReduce                                                                                                |
   |                 |                 |                 | -  Spark                                                                                                    |
   |                 |                 |                 | -  Hive (not supported currently)                                                                           |
   |                 |                 |                 | -  hql                                                                                                      |
   |                 |                 |                 | -  DistCp                                                                                                   |
   |                 |                 |                 | -  SparkScript                                                                                              |
   |                 |                 |                 | -  SparkSql (not supported in this API currently)                                                           |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+
   | description     | No              | String          | Job object description                                                                                      |
   |                 |                 |                 |                                                                                                             |
   |                 |                 |                 | Contains a maximum of 65535 characters.                                                                     |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------+

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

      The request example of MapReduce job:
      {
          "name": "my-mapreduce-job",
          "mains": [ ],
          "libs": [
          "092b628b-26a3-4571-9ba4-f8d000df8877"
          ],
          "is_protected": false,
          "interface": [ ],
          "is_public": false,
          "type": "MapReduce",
          "description": "This is the Map Reduce job template"
      }

      The request example of Spark job:
      {
          "name": "my-spark-job",
          "type": "Spark",
          "description": "This is the Spark job template",
          "mains": [ ],
          "libs": [
              "ed2ffd92-6308-44cb-b930-e10b6d65d3aa"
          ],
          "is_public": false,
          "is_protected": false,
          "interface": [ ]
      }

      The request example of DistCp job:
      {
          "name": "my-distcp-job",
          "type": "DistCp",
          "description": "This is the DistCp job template",
          "mains": [ ],
          "libs": [ ],
          "is_public": false,
          "is_protected": false,
          "interface": [ ]
      }

      The request example of Hive job:
      {
          "name": "my-hive-job",
          "type": "Hive",
          "description": "This is the Hive job template",
      "mains": [
          "0d58a7e1-3ea7-413e-9a94-7702f99a9fa2"
      ],
          "libs": [ ],
          "is_public": false,
          "is_protected": false,
          "interface": [ ]
      }

      The request example of SparkScript job:
      {
          "name": "my-sparkscript-job",
          "type": "SparkScript",
          "description": "This is the SparkScript job template",
          "mains": [
          "89e6a8bc-dde1-4053-97c1-72504f630dbf"
          ],
          "libs": [ ],
          "is_public": false,
          "is_protected": false,
          "interface": [ ]
      }

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

:ref:`Table 4 <mrs_02_0041__table1584477916050>` describes the status code of this API.

.. _mrs_02_0041__table1584477916050:

.. table:: **Table 4** Status code

   =========== =============================================
   Status code Description
   =========== =============================================
   202         The job object has been successfully created.
   =========== =============================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
