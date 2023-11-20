:original_name: mrs_02_0087.html

.. _mrs_02_0087:

Querying a List of Jobs
=======================

Function
--------

This API is used to query the job list in an MRS cluster.

URI
---

-  Format

   GET /v2/{project_id}/clusters/{cluster_id}/job-executions

-  Parameter description

   .. table:: **Table 1** URI parameter

      +------------+-----------+-----------------------------------------------------------------------------------------------------------------------------------+
      | Name       | Mandatory | Description                                                                                                                       |
      +============+===========+===================================================================================================================================+
      | project_id | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`.                         |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------------------------------+
      | cluster_id | Yes       | Cluster ID. For details on how to obtain the cluster ID, see :ref:`Obtaining a Cluster ID <mrs_02_0091__section177891315153619>`. |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------------------------------+

Request
-------

.. table:: **Table 2** Request parameter description

   +----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | Parameter            | Mandatory       | Type            | Description                                                                                                   |
   +======================+=================+=================+===============================================================================================================+
   | job_name             | No              | String          | Job name. It contains 1 to 64 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed. |
   +----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | job_type             | No              | String          | Type of a job.                                                                                                |
   |                      |                 |                 |                                                                                                               |
   |                      |                 |                 | -  MapReduce                                                                                                  |
   |                      |                 |                 | -  SparkSubmit                                                                                                |
   |                      |                 |                 | -  HiveScript                                                                                                 |
   |                      |                 |                 | -  HiveSql                                                                                                    |
   |                      |                 |                 | -  DistCp, importing and exporting data                                                                       |
   |                      |                 |                 | -  SparkScript                                                                                                |
   |                      |                 |                 | -  SparkSql                                                                                                   |
   |                      |                 |                 | -  Flink                                                                                                      |
   +----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | job_state            | No              | String          | Execution status of a job.                                                                                    |
   |                      |                 |                 |                                                                                                               |
   |                      |                 |                 | -  **FAILED**: indicates that the job fails to be executed.                                                   |
   |                      |                 |                 | -  **KILLED**: indicates that the job is terminated.                                                          |
   |                      |                 |                 | -  **New**: indicates that the job is created.                                                                |
   |                      |                 |                 | -  **NEW_SAVING**: indicates that the job has been created and is being saved.                                |
   |                      |                 |                 | -  **SUBMITTED**: indicates that the job is submitted.                                                        |
   |                      |                 |                 | -  **ACCEPTED**: indicates that the job is accepted.                                                          |
   |                      |                 |                 | -  **RUNNING**: indicates that the job is running.                                                            |
   |                      |                 |                 | -  **FINISHED**: indicates that the job is completed.                                                         |
   +----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | job_result           | No              | String          | Execution result of a job.                                                                                    |
   |                      |                 |                 |                                                                                                               |
   |                      |                 |                 | -  **FAILED**: indicates that the job fails to be executed.                                                   |
   |                      |                 |                 | -  **KILLED**: indicates that the job is manually terminated during execution.                                |
   |                      |                 |                 | -  **UNDEFINED**: indicates that the job is being executed.                                                   |
   |                      |                 |                 | -  **SUCCEEDED**: indicates that the job has been successfully executed.                                      |
   +----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | limit                | No              | Integer         | Number of records displayed on each page in the returned result. The default value is **10**.                 |
   +----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | offset               | No              | Integer         | Offset.                                                                                                       |
   |                      |                 |                 |                                                                                                               |
   |                      |                 |                 | The default offset from which the job list starts to be queried is **1**.                                     |
   +----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | sort_by              | No              | String          | Ranking mode of returned results. The default value is **desc**.                                              |
   |                      |                 |                 |                                                                                                               |
   |                      |                 |                 | -  **asc**: indicates that the returned results are ranked in ascending order.                                |
   |                      |                 |                 | -  **desc**: indicates that the returned results are ranked in descending order.                              |
   +----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | submitted_time_begin | No              | TimeStamp       | UTC timestamp after which a job is submitted, in milliseconds. For example, 1562032041362.                    |
   +----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+
   | submitted_time_end   | No              | TimeStamp       | UTC timestamp before which a job is submitted, in milliseconds. For example, 1562032041362.                   |
   +----------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------+

Response
--------

.. table:: **Table 3** Response parameter description

   +--------------+---------+-----------------------------------------------------------------------------------------------+
   | Parameter    | Type    | Description                                                                                   |
   +==============+=========+===============================================================================================+
   | total_record | Integer | Total number of jobs                                                                          |
   +--------------+---------+-----------------------------------------------------------------------------------------------+
   | job_list     | Array   | Job list. For details about the parameter, see :ref:`Table 4 <mrs_02_0087__table9145123857>`. |
   +--------------+---------+-----------------------------------------------------------------------------------------------+

.. _mrs_02_0087__table9145123857:

.. table:: **Table 4** Job parameter description

   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                                    |
   +=======================+=======================+================================================================================================================================================================================================================+
   | job_id                | String                | Job ID                                                                                                                                                                                                         |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | user                  | String                | Name of the user who submits a job.                                                                                                                                                                            |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_name              | String                | Job name. It contains 1 to 64 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed.                                                                                                  |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_result            | String                | Final result of a job.                                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                                |
   |                       |                       | -  **FAILED**: indicates that the job fails to be executed.                                                                                                                                                    |
   |                       |                       | -  **KILLED**: indicates that the job is manually terminated during execution.                                                                                                                                 |
   |                       |                       | -  **UNDEFINED**: indicates that the job is being executed.                                                                                                                                                    |
   |                       |                       | -  **SUCCEEDED**: indicates that the job has been successfully executed.                                                                                                                                       |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_state             | String                | Execution status of a job.                                                                                                                                                                                     |
   |                       |                       |                                                                                                                                                                                                                |
   |                       |                       | -  **FAILED**: indicates that the job fails to be executed.                                                                                                                                                    |
   |                       |                       | -  **KILLED**: indicates that the job is terminated.                                                                                                                                                           |
   |                       |                       | -  **New**: indicates that the job is created.                                                                                                                                                                 |
   |                       |                       | -  **NEW_SAVING**: indicates that the job has been created and is being saved.                                                                                                                                 |
   |                       |                       | -  **SUBMITTED**: indicates that the job is submitted.                                                                                                                                                         |
   |                       |                       | -  **ACCEPTED**: indicates that the job is accepted.                                                                                                                                                           |
   |                       |                       | -  **RUNNING**: indicates that the job is running.                                                                                                                                                             |
   |                       |                       | -  **FINISHED**: indicates that the job is completed.                                                                                                                                                          |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_progress          | Float                 | Job execution progress.                                                                                                                                                                                        |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_type              | String                | Type of a job.                                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                                |
   |                       |                       | -  MapReduce                                                                                                                                                                                                   |
   |                       |                       | -  SparkSubmit                                                                                                                                                                                                 |
   |                       |                       | -  HiveScript                                                                                                                                                                                                  |
   |                       |                       | -  HiveSql                                                                                                                                                                                                     |
   |                       |                       | -  DistCp, importing and exporting data                                                                                                                                                                        |
   |                       |                       | -  SparkScript                                                                                                                                                                                                 |
   |                       |                       | -  SparkSql                                                                                                                                                                                                    |
   |                       |                       | -  Flink                                                                                                                                                                                                       |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | started_time          | Long                  | Start time to run a job. Unit: milliseconds                                                                                                                                                                    |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | submitted_time        | Long                  | Time when a job is submitted. Unit: milliseconds                                                                                                                                                               |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | finished_time         | Long                  | End time to run a job. Unit: milliseconds                                                                                                                                                                      |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | elapsed_time          | Long                  | Running duration of a job. Unit: milliseconds                                                                                                                                                                  |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | arguments             | Array                 | Run parameters. The parameter contains a maximum of 4,096 characters, excluding special characters such as ``;|&>'<$,`` and can be left blank.                                                                 |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | properties            | Object                | Configuration parameter, which is used to configure **-d** parameters. The parameter contains a maximum of 2,048 characters, excluding special characters such as :literal:`><|'`&!\\,` and can be left blank. |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | launcher_id           | String                | Launcher job ID.                                                                                                                                                                                               |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | app_id                | String                | Actual job ID.                                                                                                                                                                                                 |
   +-----------------------+-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   None.

-  Example response

   -  Example of a successful response

      .. code-block::

         {
             "total_record": 2,
             "job_list": [{
                     "job_id": "981374c1-85da-44ee-be32-edfb4fba776c",
                     "user": "xxxx",
                     "job_name": "SparkSubmitTset",
                     "job_result": "UNDEFINED",
                     "job_state": "ACCEPTED",
                     "job_progress": 0,
                     "job_type": "SparkSubmit",
                     "started_time": 0,
                     "submitted_time": 1564714763119,
                     "finished_time": 0,
                     "elapsed_time": 0,
                     "queue": "default",
                     "arguments": "[--class, --driver-memory, --executor-cores, --master, yarn-cluster, obs://obs-test/hadoop-mapreduce-examples-3.1.1.jar, dddd]",
                     "launcher_id": "application_1564622673393_0613",
                     "properties": "{}"
                 },
                 {
                     "job_id": "c54c8aa0-c277-4f83-8acc-521d85cfa32b",
                     "user": "xxxx",
                     "job_name": "SparkSubmitTset2",
                     "job_result": "UNDEFINED",
                     "job_state": "ACCEPTED",
                     "job_progress": 0,
                     "job_type": "SparkSubmit",
                     "started_time": 0,
                     "submitted_time": 1564714020099,
                     "finished_time": 0,
                     "elapsed_time": 0,
                     "queue": "default",
                     "arguments": "[--conf, yujjsjhe, --driver-memory, yueujdjjd, --master, yarn-cluster, obs://obs-test/hadoop-mapreduce-examples-3.1.1.jar]",
                     "launcher_id": "application_1564622673393_0611",
                     "properties": "{}"
                 }
             ]
         }

   -  Example of a failed response

      .. code-block::

         {
         "error_msg": "Failed to query the job list."
         "error_code":"0166"
         }

Status Code
-----------

For details about status codes, see :ref:`Status Codes <mrs_02_0015>`.

.. note::

   A regular GET request. The response code is 200 if the request is successful. The response code is 202 if the request is accepted but not completed.
