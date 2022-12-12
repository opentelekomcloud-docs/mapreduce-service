:original_name: mrs_02_0043.html

.. _mrs_02_0043:

Executing a Job Object
======================

Function
--------

This API is used to execute a created job object. This API is compatible with Sahara.

URI
---

-  Format

   POST /v1.1/{project_id}/jobs/{job_id}/execute

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

   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                          |
   +=================+=================+=================+======================================================================================================================================================================================+
   | cluster_id      | Yes             | String          | Cluster ID                                                                                                                                                                           |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | input_id        | Yes             | String          | Input data source ID of a job object                                                                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                      |
   |                 |                 |                 | For details on how to obtain the input data source ID, see :ref:`Creating a Data Source <mrs_02_0022>`.                                                                              |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | output_id       | Yes             | String          | Output data source ID of a job object                                                                                                                                                |
   |                 |                 |                 |                                                                                                                                                                                      |
   |                 |                 |                 | For details on how to obtain the output data source ID, see :ref:`Creating a Data Source <mrs_02_0022>`.                                                                             |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | is_protected    | No              | Bool            | Whether a job object is protected                                                                                                                                                    |
   |                 |                 |                 |                                                                                                                                                                                      |
   |                 |                 |                 | -  true                                                                                                                                                                              |
   |                 |                 |                 | -  false                                                                                                                                                                             |
   |                 |                 |                 |                                                                                                                                                                                      |
   |                 |                 |                 | The current version does not support this function.                                                                                                                                  |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | is_public       | No              | Bool            | Whether a job object is public                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                      |
   |                 |                 |                 | -  true                                                                                                                                                                              |
   |                 |                 |                 | -  false                                                                                                                                                                             |
   |                 |                 |                 |                                                                                                                                                                                      |
   |                 |                 |                 | The current version does not support this function.                                                                                                                                  |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_configs     | Yes             | Object          | Key-value pair set for saving job running configurations                                                                                                                             |
   |                 |                 |                 |                                                                                                                                                                                      |
   |                 |                 |                 | If the job type is MapReduce or Spark, set the first parameter of **args** to be the same as the **arguments** parameter in :ref:`Adding a Job and Executing the Job <mrs_02_0040>`. |
   +-----------------+-----------------+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response
--------

.. table:: **Table 3** Response parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                               |
   +=======================+=======================+===========================================================================================================+
   | output_id             | String                | Output data source ID of a job object                                                                     |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | info                  | Object                | Job object status information                                                                             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | job_id                | String                | Job object ID                                                                                             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | tenant_id             | String                | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | created_at            | String                | Job object creation time                                                                                  |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | updated_at            | String                | Job object update time                                                                                    |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | return_code           | String                | Response code after job execution                                                                         |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | oozie_job_id          | String                | Workflow ID returned by Oozie                                                                             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_protected          | Bool                  | Whether a job object is protected                                                                         |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | input_id              | String                | Input data source ID of a job object                                                                      |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | cluster_id            | String                | Cluster ID                                                                                                |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_public             | Bool                  | Whether a job object is public                                                                            |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | job_configs           | Object                | Key-value pair set for saving job running configurations                                                  |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | id                    | String                | Job object ID                                                                                             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   .. code-block::

      The request example of MapReduce job:
      {
          "cluster_id": "811e1134-666f-4c48-bc92-afb5b10c9d8c",
          "input_id": "3e1bc8e6-8c69-4749-8e52-90d9341d15bc",
          "output_id": "52146b52-6540-4aac-a024-fee253cf52a9",
          "is_protected": false,
          "is_public": false,
          "job_configs": {
              "configs": {
                 "mapred.map.tasks": "1",
                 "mapred.reduce.tasks": "1"
             },
             "args": [
                 "wordcount",
                 "arg2"
             ],
             "params": {
                "param2": "value2",
                "param1": "value1"
             }
          }
      }

      The request example of Spark job:
      {
          "cluster_id": "8f3a547d-d53a-44ba-9aad-ded0b0b26e9c",
          "input_id": "3e1bc8e6-8c69-4749-8e52-90d9341d15bc",
          "output_id": "8bb0259f-309a-49f4-843b-0be86ac1623a",
          "job_configs": {
              "configs": { },
              "args": [
                  "org.apache.spark.examples.SparkPi 10",
                  "arg2"
              ],
              "params": {
                  "param2": "value2",
                  "param1": "value1"
              }
          }
      }

      The request example of DistCp job:
      {
          "cluster_id": "811e1134-666f-4c48-bc92-afb5b10c9d8c",
          "input_id": "3e1bc8e6-8c69-4749-8e52-90d9341d15bc",
          "output_id": "52146b52-6540-4aac-a024-fee253cf52a9",
          "is_protected": false,
          "is_public": false,
          "job_configs": {
              "configs": { },
             "args": [
                 "arg1",
                 "arg2"
             ],
             "params": {
                "param2": "value2",
                "param1": "value1"
             }
          }
      }

      The request example of Hive job:
      {
          "cluster_id": "8f3a547d-d53a-44ba-9aad-ded0b0b26e9c",
          "input_id": "3e1bc8e6-8c69-4749-8e52-90d9341d15bc",
          "output_id": "8bb0259f-309a-49f4-843b-0be86ac1623a",
          "is_protected": false,
          "is_public": false,
          "job_configs": {
              "configs": { },
             "args": [
                 "arg1",
                 "arg2"
             ],
             "params": {
                "param2": "value2",
                "param1": "value1"
             }
          }
      }

      The request example of SparkScript job:
      {
          "cluster_id": "811e1134-666f-4c48-bc92-afb5b10c9d8c",
          "input_id": "3e1bc8e6-8c69-4749-8e52-90d9341d15bc",
          "output_id": "52146b52-6540-4aac-a024-fee253cf52a9",
          "is_protected": false,
          "is_public": false,
          "job_configs": {
              "configs": { },
             "args": [
                 "arg1",
                 "arg2"
             ],
             "params": {
                "param2": "value2",
                "param1": "value1"
             }
          }
      }

-  Example response

   .. code-block::

      {
          "job_execution":{
              "created_at":"2017-02-20T09:11:32",
              "updated_at":"2017-02-20T09:11:32",
              "id":"4a56525d-34db-43e3-99c9-af67491025cd",
              "tenant_id":"3f99e3319a8943ceb15c584f3325d064",
              "job_id":"2c12ff33-da22-47b1-b51f-2828c16bbad8",
              "start_time":"2017-02-20T09:11:32",
              "end_time":null,
              "cluster_id":"c1000b4f-f2a1-49e1-af3c-2e19fc1eb72d",
              "oozie_job_id":null,
              "return_code":null,
              "input_id":"ce8c2b04-f46c-4580-8b58-5b6aaf4a44a9",
              "output_id":"9d59ce5b-d0f4-46d4-8738-6e50c2a5c68a",
              "is_protected":null,
              "is_public":null,
              "job_configs":{
                  "configs":{
                      "mapred.map.tasks":"1",
                      "mapred.reduce.tasks":"1"
                  },
                  "args":[
                      "wordcount ",
                      "arg2"
                  ],
                  "params":{
                      "param2":"value2",
                      "param1":"value1"
                  }
              },
              "data_source_urls":null,
              "info":null
          }
      }

Status Code
-----------

:ref:`Table 4 <mrs_02_0043__table1584477916050>` describes the status code of this API.

.. _mrs_02_0043__table1584477916050:

.. table:: **Table 4** Status code

   =========== ==============================================
   Status code Description
   =========== ==============================================
   202         The job object has been executed successfully.
   =========== ==============================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
