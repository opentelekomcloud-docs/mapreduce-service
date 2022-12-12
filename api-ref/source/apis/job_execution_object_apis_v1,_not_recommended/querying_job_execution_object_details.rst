:original_name: mrs_02_0051.html

.. _mrs_02_0051:

Querying Job Execution Object Details
=====================================

Function
--------

This API is used to query detailed information about a job execution object. This API is compatible with Sahara.

URI
---

-  Format

   GET /v1.1/{project_id}/job-executions/{job_execution_id}

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +------------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Parameter        | Mandatory | Description                                                                                               |
      +==================+===========+===========================================================================================================+
      | project_id       | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +------------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | job_execution_id | Yes       | Job execution object ID                                                                                   |
      +------------------+-----------+-----------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

None.

Response
--------

.. table:: **Table 2** Response parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                               |
   +=======================+=======================+===========================================================================================================+
   | info                  | String                | Key-value pair set, containing job running information returned by Oozie                                  |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | cluster_id            | String                | Cluster ID                                                                                                |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | job_id                | String                | Job ID                                                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | engine_job_id         | String                | Workflow ID of Oozie                                                                                      |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | oozie_job_id          | String                | Workflow ID returned by Oozie                                                                             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | tenant_id             | String                | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | created_at            | String                | Job execution object creation time                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | updated_at            | String                | Job execution object update time                                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | start_time            | String                | Job start time                                                                                            |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | end_time              | String                | Job end time                                                                                              |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | return_code           | String                | Response code after job execution                                                                         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | input_id              | String                | Input data source ID of a job execution object                                                            |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | output_id             | String                | Output data source ID of a job execution object                                                           |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_protected          | Bool                  | Whether a job execution object is protected                                                               |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_public             | Bool                  | Whether a job execution object is public                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | job_configs           | Object                | Key-value pair set for saving job running configurations                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | For details, see :ref:`Table 3 <mrs_02_0051__table2159451151623>`.                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | data_source_urls      | Object                | Data source URL of a job execution object                                                                 |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | Id                    | String                | Job execution object ID                                                                                   |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+

.. _mrs_02_0051__table2159451151623:

.. table:: **Table 3** **job_configs** parameter description

   ========= ====== =======================================
   Parameter Type   Description
   ========= ====== =======================================
   configs   Object Key-value pair set configured for a job
   args      Array  List of arguments
   params    Object Key-value pair set for running a job
   ========= ====== =======================================

Example
-------

-  Example request

   None.

-  Example response

   .. code-block::

      {
          "job_execution": {
              "created_at": "2017-06-22T06:23:51",
              "updated_at": "2017-06-22T06:23:51",
              "id": "852042ea-a32c-424b-aacf-df2e6d6642b5",
              "tenant_id": "5a3314075bfa49b9ae360f4ecd333695",
              "job_id": "",
              "start_time": "2017-06-22T06:23:51",
              "end_time": null,
              "cluster_id": "33dff020-7f96-4270-9c3a-88b99627f6e2",
              "oozie_job_id": null,
              "return_code": null,
              "input_id": null,
              "output_id": null,
              "is_protected": false,
              "is_public": null,
              "engine_job_id": null,
              "job_configs": null,
              "data_source_urls": null,
              "info": null
          }
      }

Status Code
-----------

:ref:`Table 4 <mrs_02_0051__table1584477916050>` describes the status code of this API.

.. _mrs_02_0051__table1584477916050:

.. table:: **Table 4** Status code

   =========== ==========================================================
   Status Code Description
   =========== ==========================================================
   200         The job execution object details are queried successfully.
   =========== ==========================================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
