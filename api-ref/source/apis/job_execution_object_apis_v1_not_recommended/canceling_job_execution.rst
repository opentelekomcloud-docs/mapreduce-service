:original_name: mrs_02_0052.html

.. _mrs_02_0052:

Canceling Job Execution
=======================

Function
--------

This API is used to cancel a job object being executed. This API is compatible with Sahara.

URI
---

-  Format

   GET /v1.1/{project_id}/job-executions/{job_execution_id}/cancel

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
   | end_time              | Bool                  | Job end time                                                                                              |
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
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | id                    | String                | Job execution object ID                                                                                   |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | oozie_job_id          | String                | Workflow ID returned by Oozie                                                                             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | info                  | String                | Key-value pair set, containing job running information returned by Oozie                                  |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   None.

-  Example response

   .. code-block::

      {
          "job_execution": {
              "created_at": "2017-05-25T07:28:12",
              "updated_at": "2017-05-25T07:28:13",
              "id": "2de74673-1a78-48af-a95b-e1fec4a4ae9c",
              "tenant_id": "37caa80116e1403ab603e5eeb48a2f74",
              "job_id": "",
              "start_time": "2017-05-25T07:28:12",
              "end_time": null,
              "cluster_id": "ef7b54f2-3d92-49b2-a6d7-94607e1ea7df",
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

:ref:`Table 3 <mrs_02_0052__table1584477916050>` describes the status code of this API.

.. _mrs_02_0052__table1584477916050:

.. table:: **Table 3** Status code

   +-------------+---------------------------------------------------------------+
   | Status Code | Description                                                   |
   +=============+===============================================================+
   | 200         | The job object being executed has been canceled successfully. |
   +-------------+---------------------------------------------------------------+

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
