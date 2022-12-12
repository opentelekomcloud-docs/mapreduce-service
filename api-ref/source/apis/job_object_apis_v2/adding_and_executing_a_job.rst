:original_name: mrs_02_0085.html

.. _mrs_02_0085:

Adding and Executing a Job
==========================

Function
--------

This API is used to add and submit a job in an MRS cluster.

.. note::

   -  If Kerberos authentication is enabled for a cluster, on the **Dashboard** tab page of the cluster details page, click **Click to synchronize** on the right side of **IAM User Sync** to synchronize IAM users, and then submit a job through this API.

URI
---

-  Format

   POST /v2/{project_id}/clusters/{cluster_id}/job-executions

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +------------+-----------+-----------------------------------------------------------------------------------------------------------------------------------+
      | Parameter  | Mandatory | Description                                                                                                                       |
      +============+===========+===================================================================================================================================+
      | project_id | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`.                         |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------------------------------+
      | cluster_id | Yes       | Cluster ID. For details on how to obtain the cluster ID, see :ref:`Obtaining a Cluster ID <mrs_02_0091__section177891315153619>`. |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------------------------------+

Request
-------

.. table:: **Table 2** Request parameter description

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   +=================+=================+=================+=================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | job_type        | Yes             | String          | Type of a job.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                 | -  MapReduce                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   |                 |                 |                 | -  SparkSubmit                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                 |                 |                 | -  HiveScript                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                 |                 |                 | -  HiveSql                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
   |                 |                 |                 | -  DistCp, importing and exporting data                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |                 |                 |                 | -  SparkScript                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                 |                 |                 | -  SparkSql                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
   |                 |                 |                 | -  Flink                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                 |    Spark, Hive, and Flink jobs can be added to only clusters that include Spark, Hive, and Flink components.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_name        | Yes             | String          | Job name. It contains 1 to 64 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed.                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                 |    Identical job names are allowed but not recommended.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | arguments       | No              | Array           | Key parameter for program execution. The parameter is specified by the function of the user's program. MRS is only responsible for loading the parameter.                                                                                                                                                                                                                                                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                 | The parameter contains a maximum of 4,096 characters, excluding special characters such as ``;|&>'<$,`` and can be left blank.                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                 |    -  If you enter a parameter with sensitive information (such as the login password), the parameter may be exposed in the job details display and log printing. Exercise caution when performing this operation.                                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                 |    -  For MRS 1.9.2 or later, a file path on OBS can start with **obs://**. To use this format to submit HiveScript or HiveSQL jobs, choose **Components** > **Hive** > **Service Configuration** on the cluster details page, set **Type** to **All**, and search for **core.site.customized.configs**. Add the endpoint configuration item (**fs.obs.endpoint**) of OBS and enter the endpoint corresponding to OBS in **Value**. Obtain the value from `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__. |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | properties      | No              | Object          | Program system parameter.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                 | The parameter contains a maximum of 2,048 characters, excluding special characters such as :literal:`><|'`&!\\,` and can be left blank.                                                                                                                                                                                                                                                                                                                                                                                                         |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response
--------

.. table:: **Table 3** Response parameter description

   +-----------------------+-----------------------+---------------------------------------------------------+
   | Parameter             | Type                  | Description                                             |
   +=======================+=======================+=========================================================+
   | job_submit_result     | Object                | Job execution result                                    |
   +-----------------------+-----------------------+---------------------------------------------------------+
   | job_id                | String                | Job ID                                                  |
   +-----------------------+-----------------------+---------------------------------------------------------+
   | state                 | String                | Job submission status.                                  |
   |                       |                       |                                                         |
   |                       |                       | -  **COMPLETE**: The job is submitted.                  |
   |                       |                       | -  **JOBSTAT_SUBMIT_FAILED**: Failed to submit the job. |
   +-----------------------+-----------------------+---------------------------------------------------------+
   | error_msg             | String                | Error message                                           |
   +-----------------------+-----------------------+---------------------------------------------------------+
   | error_code            | String                | Error code                                              |
   +-----------------------+-----------------------+---------------------------------------------------------+

Example
-------

-  Example request

   The following is an example of an MapReduce job request:

   .. code-block::

      {
          "job_name":"MapReduceTest",
          "job_type":"MapReduce",
          "arguments":[
              "obs://obs-test/program/hadoop-mapreduce-examples-x.x.x.jar",
              "wordcount",
              "obs://obs-test/input/",
              "obs://obs-test/job/mapreduce/output"
          ],
          "properties":{
              "fs.obs.endpoint":"obs endpoint",
              "fs.obs.access.key":"xxx",
              "fs.obs.secret.key":"yyy"
          }
      }

   The following is an example of a SparkSubmit job request:

   .. code-block::

      {
          "job_name":"SparkSubmitTest",
          "job_type":"SparkSubmit",
          "arguments":[
              "--master",
              "yarn",
              "--deploy-mode",
              "cluster",
              "--py-files",
              "obs://obs-test/a.py",
              "--conf",
              "spark.yarn.appMasterEnv.PYTHONPATH=/tmp:$PYTHONPATH",
              "--conf",
              "spark.yarn.appMasterEnv.aaa=aaaa",
              "--conf",
              "spark.executorEnv.aaa=executoraaa",
              "--properties-file",
              "obs://obs-test/test-spark.conf",
              "obs://obs-test/pi.py",
              "100000"
          ],
          "properties":{
              "fs.obs.access.key":"xxx",
              "fs.obs.secret.key":"yyy"
          }
      }

   The following is an example of a HiveScript job request:

   .. code-block::

      {
          "job_name":"HiveScriptTest",
          "job_type":"HiveScript",
          "arguments":[
              "obs://obs-test/sql/test_script.sql"
          ],
          "properties":{
              "fs.obs.endpoint":"obs endpoint",
              "fs.obs.access.key":"xxx",
              "fs.obs.secret.key":"yyy"
          }
      }

   The following is an example of a HiveSQL job request:

   .. code-block::

      {
          "job_name":"HiveSqlTest",
          "job_type":"HiveSql",
          "arguments":[
              "DROP TABLE IF EXISTS src_wordcount;create external table src_wordcount(line string);insert into src_wordcount values('v1')"
          ],
          "properties":{
              "fs.obs.endpoint":"obs endpoint",
              "fs.obs.access.key":"xxx",
              "fs.obs.secret.key":"yyy"
          }
      }

   The following is an example of a DistCp job request:

   .. code-block::

      {
          "job_name":"DistCpTest",
          "job_type":"DistCp",
          "arguments":[
              "obs://obs-test/DistcpJob/",
              "/user/test/sparksql/"
          ],
          "properties":{
              "fs.obs.endpoint":"obs endpoint",
              "fs.obs.access.key":"xxx",
              "fs.obs.secret.key":"yyy"
          }
      }

   The following is an example of a SparkScript job request:

   .. code-block::

      {
          "job_name":"SparkScriptTest",
          "job_type":"SparkScript",
          "arguments":[
              "op-key1",
              "op-value1",
              "op-key2",
              "op-value2",
              "obs://obs-test/sql/test_script.sql"
          ],
          "properties":{
              "fs.obs.access.key":"xxx",
              "fs.obs.secret.key":"yyy"
          }
      }

   The following is an example of a SparkSQL job request:

   .. code-block::

      {
          "job_name":"SparkSqlTest",
          "job_type":"SparkSql",
          "arguments":[
              "op-key1",
              "op-value1",
              "op-key2",
              "op-value2",
              "create table student_info3 (id string,name string,gender string,age int,addr string);"
          ],
          "properties":{
              "fs.obs.access.key":"xxx",
              "fs.obs.secret.key":"yyy"
          }
      }

   The following is an example of a Flink job request:

   .. code-block::

      {
          "job_name":"FlinkTest",
          "job_type":"Flink",
          "arguments":[
              "run",
              "-d",
              "-ynm",
              "testExcutorejobhdfsbatch",
              "-m",
              "yarn-cluster",
              "hdfs://test/examples/batch/WordCount.jar"
          ],
          "properties":{
              "fs.obs.endpoint":"obs endpoint",
              "fs.obs.access.key":"xxx",
              "fs.obs.secret.key":"yyy"
          }
      }

-  Example response

   -  Example of a successful response

      .. code-block::

         {
           "job_submit_result":{
               "job_id":"44b37a20-ffe8-42b1-b42b-78a5978d7e40",
               "state":"COMPLETE"
           }
         }

   -  Example of a failed response

      .. code-block::

         {
         "error_msg": Hive jobs cannot be submitted.
         "error_code":"0168"
         }

Status Code
-----------

For details about status codes, see :ref:`Status Codes <mrs_02_0015>`.
