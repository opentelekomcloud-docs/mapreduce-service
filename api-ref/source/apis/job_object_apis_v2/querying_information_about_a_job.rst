:original_name: mrs_02_0086.html

.. _mrs_02_0086:

Querying Information About a Job
================================

Function
--------

This API is used to query information about a specified job in an MRS cluster.

URI
---

-  Format

   GET /v2/{project_id}/clusters/{cluster_id}/job-executions/{job_execution_id}

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +------------------+-----------+-----------------------------------------------------------------------------------------------------------------------------------+
      | Parameter        | Mandatory | Description                                                                                                                       |
      +==================+===========+===================================================================================================================================+
      | project_id       | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`.                         |
      +------------------+-----------+-----------------------------------------------------------------------------------------------------------------------------------+
      | cluster_id       | Yes       | Cluster ID. For details on how to obtain the cluster ID, see :ref:`Obtaining a Cluster ID <mrs_02_0091__section177891315153619>`. |
      +------------------+-----------+-----------------------------------------------------------------------------------------------------------------------------------+
      | job_execution_id | Yes       | Job ID. For details on how to obtain the job ID, see :ref:`Obtaining a Job ID <mrs_02_0091__section247234143612>`.                |
      +------------------+-----------+-----------------------------------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

None.

Response
--------

.. table:: **Table 2** Response parameter description

   +------------+--------+------------------------------------------------------------------------------------------------------+
   | Parameter  | Type   | Description                                                                                          |
   +============+========+======================================================================================================+
   | job_detail | Object | Job details. For details about the parameter, see :ref:`Table 3 <mrs_02_0086__table12040613193927>`. |
   +------------+--------+------------------------------------------------------------------------------------------------------+

.. _mrs_02_0086__table12040613193927:

.. table:: **Table 3** Job parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                     |
   +=======================+=======================+=================================================================================================================================================================================================================+
   | job_id                | String                | Job ID.                                                                                                                                                                                                         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | user                  | String                | Name of the user who submits a job.                                                                                                                                                                             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_name              | String                | Job name. It contains 1 to 64 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed.                                                                                                   |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_result            | String                | Final result of a job.                                                                                                                                                                                          |
   |                       |                       |                                                                                                                                                                                                                 |
   |                       |                       | -  **FAILED**: indicates that the job fails to be executed.                                                                                                                                                     |
   |                       |                       | -  **KILLED**: indicates that the job is manually terminated during execution.                                                                                                                                  |
   |                       |                       | -  **UNDEFINED**: indicates that the job is being executed.                                                                                                                                                     |
   |                       |                       | -  **SUCCEEDED**: indicates that the job has been successfully executed.                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_state             | String                | Execution status of a job.                                                                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                                 |
   |                       |                       | -  FAILED: failed                                                                                                                                                                                               |
   |                       |                       | -  **KILLED**: indicates that the job is terminated.                                                                                                                                                            |
   |                       |                       | -  **New**: indicates that the job is created.                                                                                                                                                                  |
   |                       |                       | -  **NEW_SAVING**: indicates that the job has been created and is being saved.                                                                                                                                  |
   |                       |                       | -  **SUBMITTED**: indicates that the job is submitted.                                                                                                                                                          |
   |                       |                       | -  **ACCEPTED**: indicates that the job is accepted.                                                                                                                                                            |
   |                       |                       | -  **RUNNING**: indicates that the job is running.                                                                                                                                                              |
   |                       |                       | -  **FINISHED**: indicates that the job is completed.                                                                                                                                                           |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_progress          | Float                 | Job execution progress.                                                                                                                                                                                         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_type              | String                | Type of a job.                                                                                                                                                                                                  |
   |                       |                       |                                                                                                                                                                                                                 |
   |                       |                       | -  MapReduce                                                                                                                                                                                                    |
   |                       |                       | -  SparkSubmit                                                                                                                                                                                                  |
   |                       |                       | -  HiveScript                                                                                                                                                                                                   |
   |                       |                       | -  HiveSql                                                                                                                                                                                                      |
   |                       |                       | -  DistCp, importing and exporting data                                                                                                                                                                         |
   |                       |                       | -  SparkScript                                                                                                                                                                                                  |
   |                       |                       | -  SparkSql                                                                                                                                                                                                     |
   |                       |                       | -  Flink                                                                                                                                                                                                        |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | started_time          | Long                  | Start time to run a job. Unit: ms.                                                                                                                                                                              |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | submitted_time        | Long                  | Time when a job is submitted. Unit: ms.                                                                                                                                                                         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | finished_time         | Long                  | End time to run a job. Unit: ms.                                                                                                                                                                                |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | elapsed_time          | Long                  | Running duration of a job. Unit: ms.                                                                                                                                                                            |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | arguments             | Array                 | Running parameter. The parameter contains a maximum of 4,096 characters, excluding special characters such as\ ``;|&>'<$,`` and can be left blank.                                                              |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | properties            | Object                | Configuration parameter, which is used to configure **-d** parameters. The parameter contains a maximum of 2,048 characters, excluding special characters such as\ :literal:`><|'`&!\\,` and can be left blank. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | launcher_id           | String                | Launcher job ID.                                                                                                                                                                                                |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | app_id                | String                | Actual job ID.                                                                                                                                                                                                  |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   None.

-  Example response

   -  Example of a successful response

      .. code-block::

         {
             "job_detail": {
                 "job_id": "431b135e-c090-489f-b1db-0abe3822b855",
                 "user": "xxxx",
                 "job_name": "pyspark1",
                 "job_result": "SUCCEEDED",
                 "job_state": "FINISHED",
                 "job_progress": 100,
                 "job_type": "SparkSubmit",
                 "started_time": 1564626578817,
                 "submitted_time": 1564626561541,
                 "finished_time": 1564626664930,
                 "elapsed_time": 86113,
                 "queue": "default",
                 "arguments": "[--class, org.apache.spark.examples.SparkPi, --driver-memory, 512MB, --num-executors, 1, --executor-cores, 1, --master, yarn-cluster, obs://obs-test/jobs/spark/spark-examples_2.11-2.1.0.jar, 10000]",
                 "launcher_id": "application_1564622673393_0006",
                 "app_id": "application_1564622673393_0007",
                 "properties": "{}"
             }
         }

   -  Example of a failed response

      .. code-block::

         {
         "error_msg": "Failed to query the job."
         "error_code":"0162"
         }

Status Code
-----------

For details about status codes, see :ref:`Status Codes <mrs_02_0015>`.

.. note::

   Generally, if status code 200 is returned, an API is successfully called. However, due to compatibility problems in earlier versions, the status code for a successful call of this API is 202. You can use status code 202 to check whether the response to this API is normal.
