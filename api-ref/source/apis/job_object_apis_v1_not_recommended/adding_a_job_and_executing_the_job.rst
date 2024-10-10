:original_name: mrs_02_0040.html

.. _mrs_02_0040:

Adding a Job and Executing the Job
==================================

Function
--------

This API is used to add a job to an MRS cluster and execute the job. This API is incompatible with Sahara.

URI
---

-  Format

   POST /v1.1/{project_id}/jobs/submit-job

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

   +------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter        | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                                     |
   +==================+=================+=================+=================================================================================================================================================================================================================================================================================================================================================================================+
   | job_type         | Yes             | Integer         | Job type code                                                                                                                                                                                                                                                                                                                                                                   |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | -  1: MapReduce                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | -  2: Spark                                                                                                                                                                                                                                                                                                                                                                     |
   |                  |                 |                 | -  3: Hive Script                                                                                                                                                                                                                                                                                                                                                               |
   |                  |                 |                 | -  4: HiveQL (not supported currently)                                                                                                                                                                                                                                                                                                                                          |
   |                  |                 |                 | -  5: DistCp, importing and exporting data. For details, see :ref:`Table 3 <mrs_02_0040__table3863810010324>`.                                                                                                                                                                                                                                                                  |
   |                  |                 |                 | -  6: Spark Script                                                                                                                                                                                                                                                                                                                                                              |
   |                  |                 |                 | -  7: Spark SQL, submitting Spark SQL statements. For details, see :ref:`Table 4 <mrs_02_0040__table63617887103233>`. (Not supported in this API currently.)                                                                                                                                                                                                                    |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 |    .. note::                                                                                                                                                                                                                                                                                                                                                                    |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 |       Spark and Hive jobs can be added to only clusters that include Spark and Hive components.                                                                                                                                                                                                                                                                                 |
   +------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_name         | Yes             | String          | Job name                                                                                                                                                                                                                                                                                                                                                                        |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | Contains only 1 to 64 letters, digits, hyphens (-), and underscores (_).                                                                                                                                                                                                                                                                                                        |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                                       |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 |    Identical job names are allowed but not recommended.                                                                                                                                                                                                                                                                                                                         |
   +------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cluster_id       | Yes             | String          | Cluster ID                                                                                                                                                                                                                                                                                                                                                                      |
   +------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | jar_path         | Yes             | String          | Path of the JAR or SQL file for program execution                                                                                                                                                                                                                                                                                                                               |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | The parameter must meet the following requirements:                                                                                                                                                                                                                                                                                                                             |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | -  Contains a maximum of 1,023 characters, excluding special characters such as\ ``;|&><'$.`` The address cannot be empty or full of spaces.                                                                                                                                                                                                                                    |
   |                  |                 |                 | -  Starts with **/** or **s3a://**. The OBS path does not support files or programs encrypted by KMS.                                                                                                                                                                                                                                                                           |
   |                  |                 |                 | -  Spark Script must end with **.sql** while MapReduce and Spark Jar must end with **.jar**.\ **sql** and **jar** are case-insensitive.                                                                                                                                                                                                                                         |
   +------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | arguments        | No              | String          | Key parameter for program execution. The parameter is specified by the function of the user's program. MRS is only responsible for loading the parameter.                                                                                                                                                                                                                       |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | The parameter contains a maximum of 2,047 characters, excluding special characters such as\ ``;|&>'<$,`` and can be left blank.                                                                                                                                                                                                                                                 |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                                       |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 |    When entering a parameter containing sensitive information (for example, login password), you can add an at sign (@) before the parameter name to encrypt the parameter value. This prevents the sensitive information from being persisted in plaintext. Therefore, when you view job information on the MRS, sensitive information will be displayed as asterisks (``*``). |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 |    For example, username=admin @password=admin_123.                                                                                                                                                                                                                                                                                                                             |
   +------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | input            | No              | String          | Path for inputting data, which must start with **/** or **s3a://**. Set this parameter to a correct OBS path. The OBS path does not support files or programs encrypted by KMS.                                                                                                                                                                                                 |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | The parameter contains a maximum of 1,023 characters, excluding special characters such as\ ``;|&>'<$,`` and can be left blank.                                                                                                                                                                                                                                                 |
   +------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | output           | No              | String          | Path for outputting data, which must start with **/** or **s3a://**. A correct OBS path is required. If the path does not exist, the system automatically creates it.                                                                                                                                                                                                           |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | The parameter contains a maximum of 1,023 characters, excluding special characters such as\ ``;|&>'<$,`` and can be left blank.                                                                                                                                                                                                                                                 |
   +------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_log          | No              | String          | Path for storing job logs that record job running status. The path must start with **/** or **s3a://**. A correct OBS path is required.                                                                                                                                                                                                                                         |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | The parameter contains a maximum of 1,023 characters, excluding special characters such as\ ``;|&>'<$,`` and can be left blank.                                                                                                                                                                                                                                                 |
   +------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hive_script_path | Yes             | String          | SQL program path                                                                                                                                                                                                                                                                                                                                                                |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | This parameter is needed by Spark Script and Hive Script jobs only, and must meet the following requirements:                                                                                                                                                                                                                                                                   |
   |                  |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                 |
   |                  |                 |                 | -  Contains a maximum of 1,023 characters, excluding special characters such as\ ``;|&><'$.`` The address cannot be empty or full of spaces.                                                                                                                                                                                                                                    |
   |                  |                 |                 | -  The path must start with **/** or **s3a://**. The OBS path does not support files or programs encrypted by KMS.                                                                                                                                                                                                                                                              |
   |                  |                 |                 | -  The path must end with **.sql**.\ **sql** is case-insensitive.                                                                                                                                                                                                                                                                                                               |
   +------------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0040__table3863810010324:

.. table:: **Table 3** **DistCp** parameter description

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                         |
   +=================+=================+=================+=====================================================================================================================+
   | job_name        | Yes             | String          | Job name                                                                                                            |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | Contains only 1 to 64 letters, digits, hyphens (-), and underscores (_).                                            |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | .. note::                                                                                                           |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 |    Identical job names are allowed but not recommended.                                                             |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | input           | No              | String          | Data source path                                                                                                    |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | -  When you import data, the parameter is set to an OBS path. Files or programs encrypted by KMS are not supported. |
   |                 |                 |                 | -  When you export data, the parameter is set to an HDFS path.                                                      |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | output          | No              | String          | Data receiving path                                                                                                 |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | -  When you import data, the parameter is set to an HDFS path.                                                      |
   |                 |                 |                 | -  When you export data, the parameter is set to an OBS path.                                                       |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | file_action     | Yes             | String          | Types of file operations, including:                                                                                |
   |                 |                 |                 |                                                                                                                     |
   |                 |                 |                 | -  export: Export data from HDFS to OBS.                                                                            |
   |                 |                 |                 | -  import: Import data from OBS to HDFS.                                                                            |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------+

.. _mrs_02_0040__table63617887103233:

.. table:: **Table 4** **Spark SQL** parameter description

   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   +=================+=================+=================+===========================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | hql             | Yes             | String          | Spark SQL statement, which needs Base64 encoding and decoding. **ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/** is a standard encoding table. MRS uses **ABCDEFGHILKJMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/** for Base64 encoding. The value of the **hql** parameter is generated by adding any letter to the beginning of the encoded character string. The Spark SQL statement is generated by decoding the value in the background. |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
   |                 |                 |                 | Example:                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
   |                 |                 |                 | #. Obtain the Base64 encoding tool.                                                                                                                                                                                                                                                                                                                                                                                                                                       |
   |                 |                 |                 | #. Enter the **show tables;** Spark SQL statement in the encoding tool to perform Base64 encoding.                                                                                                                                                                                                                                                                                                                                                                        |
   |                 |                 |                 | #. Obtain the encoded character string **c2hvdyB0YWLsZXM7**.                                                                                                                                                                                                                                                                                                                                                                                                              |
   |                 |                 |                 | #. At the beginning of **c2hvdyB0YWLsZXM7**, add any letter, for example, **g**. Then, the character string becomes **gc2hvdyB0YWLsZXM7**, that is, the value of the **hql** parameter.                                                                                                                                                                                                                                                                                   |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_name        | Yes             | String          | Job name. It contains 1 to 64 characters. Only letters, digits, hyphens (-), and underscores (_) are allowed.                                                                                                                                                                                                                                                                                                                                                             |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
   |                 |                 |                 | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
   |                 |                 |                 |    Identical job names are allowed but not recommended.                                                                                                                                                                                                                                                                                                                                                                                                                   |
   +-----------------+-----------------+-----------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response
--------

.. table:: **Table 5** Response parameter description

   +---------------+--------+---------------------------------------------------------------------+
   | Parameter     | Type   | Description                                                         |
   +===============+========+=====================================================================+
   | job_execution | Object | For details, see :ref:`Table 6 <mrs_02_0040__table12040613193927>`. |
   +---------------+--------+---------------------------------------------------------------------+

.. _mrs_02_0040__table12040613193927:

.. table:: **Table 6** **job_execution** parameter description

   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                                                                                                                     |
   +=======================+=======================+=================================================================================================================================================================================================+
   | templated             | Bool                  | Whether job execution objects are generated by job templates.                                                                                                                                   |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | created_at            | Integer               | Creation time, which is a 10-bit timestamp.                                                                                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | updated_at            | Integer               | Update time, which is a 10-bit timestamp.                                                                                                                                                       |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | id                    | String                | Job ID                                                                                                                                                                                          |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | tenant_id             | String                | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`.                                                                                       |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_id                | String                | Job application ID                                                                                                                                                                              |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_name              | String                | Job name                                                                                                                                                                                        |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | input_id              | String                | Data input ID                                                                                                                                                                                   |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | output_id             | String                | Data output ID                                                                                                                                                                                  |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | start_time            | Integer               | Start time of job execution, which is a 10-bit timestamp.                                                                                                                                       |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | end_time              | Integer               | End time of job execution, which is a 10-bit timestamp.                                                                                                                                         |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | cluster_id            | String                | Cluster ID                                                                                                                                                                                      |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | engine_job_id         | String                | Workflow ID of Oozie                                                                                                                                                                            |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | return_code           | Integer               | Returned code for an execution result                                                                                                                                                           |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | is_public             | Bool                  | Whether a job is public                                                                                                                                                                         |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | -  true                                                                                                                                                                                         |
   |                       |                       | -  false                                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | The current version does not support this function.                                                                                                                                             |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | is_protected          | Bool                  | Whether a job is protected                                                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | -  true                                                                                                                                                                                         |
   |                       |                       | -  false                                                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | The current version does not support this function.                                                                                                                                             |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | group_id              | String                | Group ID of a job                                                                                                                                                                               |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | jar_path              | String                | Path of the **.jar** file for program execution                                                                                                                                                 |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | input                 | String                | Address for inputting data                                                                                                                                                                      |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | output                | String                | Address for outputting data                                                                                                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_log               | String                | Address for storing job logs                                                                                                                                                                    |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_type              | Integer               | Job type code                                                                                                                                                                                   |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | -  1: MapReduce                                                                                                                                                                                 |
   |                       |                       | -  2: Spark                                                                                                                                                                                     |
   |                       |                       | -  3: Hive Script                                                                                                                                                                               |
   |                       |                       | -  4: HiveQL (not supported currently)                                                                                                                                                          |
   |                       |                       | -  5: DistCp                                                                                                                                                                                    |
   |                       |                       | -  6: Spark Script                                                                                                                                                                              |
   |                       |                       | -  7: Spark SQL (not supported in this API currently)                                                                                                                                           |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | file_action           | String                | Data import and export                                                                                                                                                                          |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | arguments             | String                | Key parameter for program execution. The parameter is specified by the function of the user's internal program. MRS is only responsible for loading the parameter. This parameter can be empty. |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_state             | Integer               | Job status code                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | -  -1: Terminated                                                                                                                                                                               |
   |                       |                       | -  1: Starting                                                                                                                                                                                  |
   |                       |                       | -  2: Running                                                                                                                                                                                   |
   |                       |                       | -  3: Completed                                                                                                                                                                                 |
   |                       |                       | -  4: Abnormal                                                                                                                                                                                  |
   |                       |                       | -  5: Error                                                                                                                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_final_status      | Integer               | Final job status                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | -  0: unfinished                                                                                                                                                                                |
   |                       |                       | -  1: terminated due to an execution error                                                                                                                                                      |
   |                       |                       | -  2: executed successfully                                                                                                                                                                     |
   |                       |                       | -  3: canceled                                                                                                                                                                                  |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hive_script_path      | String                | Address of the Hive script                                                                                                                                                                      |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | create_by             | String                | User ID for creating jobs                                                                                                                                                                       |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | This parameter is not used in the current version, but is retained for compatibility with earlier versions.                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | finished_step         | Integer               | Number of completed steps                                                                                                                                                                       |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | This parameter is not used in the current version, but is retained for compatibility with earlier versions.                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_main_id           | String                | Main ID of a job                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | This parameter is not used in the current version, but is retained for compatibility with earlier versions.                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_step_id           | String                | Step ID of a job                                                                                                                                                                                |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | This parameter is not used in the current version, but is retained for compatibility with earlier versions.                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | postpone_at           | Integer               | Delay time, which is a 10-bit timestamp.                                                                                                                                                        |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | This parameter is not used in the current version, but is retained for compatibility with earlier versions.                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | step_name             | String                | Step name of a job                                                                                                                                                                              |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | This parameter is not used in the current version, but is retained for compatibility with earlier versions.                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | step_num              | Integer               | Number of steps                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | This parameter is not used in the current version, but is retained for compatibility with earlier versions.                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | task_num              | Integer               | Number of tasks                                                                                                                                                                                 |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | This parameter is not used in the current version, but is retained for compatibility with earlier versions.                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | update_by             | String                | User ID for updating jobs                                                                                                                                                                       |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | credentials           | String                | Token                                                                                                                                                                                           |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | The current version does not support this function.                                                                                                                                             |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | user_id               | String                | User ID for creating jobs                                                                                                                                                                       |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | This parameter is not used in the current version, but is retained for compatibility with earlier versions.                                                                                     |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | job_configs           | String                | Key-value pair set for saving job running configurations                                                                                                                                        |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | extra                 | String                | Authentication information                                                                                                                                                                      |
   |                       |                       |                                                                                                                                                                                                 |
   |                       |                       | The current version does not support this function.                                                                                                                                             |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | data_source_urls      | String                | Data source URL                                                                                                                                                                                 |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | info                  | String                | Key-value pair set, containing job running information returned by Oozie                                                                                                                        |
   +-----------------------+-----------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   The following is an example of an MapReduce job request:

   .. code-block::

      {
          "job_type": 1,
          "job_name": "mrs_test_jobone_20170602_141106",
          "cluster_id": "e955a7a3-d334-4943-a39a-994976900d56",
          "jar_path": "s3a://mrs-opsadm/jarpath/hadoop-mapreduce-examples-2.7.2.jar",
          "arguments": "wordcount",
          "input": "s3a://mrs-opsadm/input/",
          "output": "s3a://mrs-opsadm/output/",
          "job_log": "s3a://mrs-opsadm/log/",
          "file_action": "",
          "hql": "",
          "hive_script_path": ""
      }

   The request example of Spark job:

   .. code-block::

      {
          "job_type": 2,
          "job_name": "mrs_test_sparkjob_20170602_141106",
          "cluster_id": "e955a7a3-d334-4943-a39a-994976900d56",
          "jar_path": "s3a://mrs-opsadm/jarpath/spark-test.jar",
          "arguments": "org.apache.spark.examples.SparkPi 10",
          "input": "",
          "output": "s3a://mrs-opsadm/output/",
          "job_log": "s3a://mrs-opsadm/log/",
          "file_action": "",
          "hql": "",
          "hive_script_path": ""
      }

   The request example of Hive Script job:

   .. code-block::

      {
          "job_type": 3,
          "job_name": "mrs_test_SparkScriptJob_20170602_141106",
          "cluster_id": "e955a7a3-d334-4943-a39a-994976900d56",
          "jar_path": "s3a://mrs-opsadm/jarpath/Hivescript.sql",
          "arguments": "",
          "input": "s3a://mrs-opsadm/input/",
          "output": "s3a://mrs-opsadm/output/",
          "job_log": "s3a://mrs-opsadm/log/",
          "file_action": "",
          "hql": "",
          "hive_script_path": "s3a://mrs-opsadm/jarpath/Hivescript.sql"
      }

   The request example of DistCp job for import:

   .. code-block::

      {
          "job_type": 5,
          "job_name": "mrs_test_importjob_20170602_141106",
          "cluster_id": "e955a7a3-d334-4943-a39a-994976900d56",
          "input": "s3a://mrs-opsadm/jarpath/hadoop-mapreduce-examples-2.7.2.jar",
          "output": "/user",
          "file_action": "import"
      }

   The request example of DistCp job for export:

   .. code-block::

      {
          "job_type": 5,
          "job_name": "mrs_test_exportjob_20170602_141106",
          "cluster_id": "e955a7a3-d334-4943-a39a-994976900d56",
          "input": "/user/hadoop-mapreduce-examples-2.7.2.jar",
          "output": "s3a://mrs-opsadm/jarpath/",
          "file_action": "export"
      }

   The request example of Spark Script job:

   .. code-block::

      {
          "job_type": 6,
          "job_name": "mrs_test_sparkscriptjob_20170602_141106",
          "cluster_id": "e955a7a3-d334-4943-a39a-994976900d56",
          "jar_path": "s3a://mrs-opsadm/jarpath/sparkscript.sql",
          "arguments": "",
          "input": "s3a://mrs-opsadm/input/",
          "output": "s3a://mrs-opsadm/output/",
          "job_log": "s3a://mrs-opsadm/log/",
          "file_action": "",
          "hql": "",
          "hive_script_path": "s3a://mrs-opsadm/jarpath/sparkscript.sql"
      }

-  Example response

   .. code-block::

      {
        "job_execution": {
          "templated": false,
          "created_at": 1496387588,
          "updated_at": 1496387588,
          "id": "12ee9ae4-6ee1-48c6-bb84-fb0b4f76cf03",
          "tenant_id": "c71ad83a66c5470496c2ed6e982621cc",
          "job_id": "",
          "job_name": "mrs_test_jobone_20170602_141106",
          "input_id": null,
          "output_id": null,
          "start_time": 1496387588,
          "end_time": null,
          "cluster_id": "e955a7a3-d334-4943-a39a-994976900d56",
          "engine_job_id": null,
          "return_code": null,
          "is_public": null,
          "is_protected": false,
          "group_id": "12ee9ae4-6ee1-48c6-bb84-fb0b4f76cf03",
          "jar_path": "s3a://mrs-opsadm/jarpath/hadoop-mapreduce-examples-2.7.2.jar",
          "input": "s3a://mrs-opsadm/input/",
          "output": "s3a://mrs-opsadm/output/",
          "job_log": "s3a://mrs-opsadm/log/",
          "job_type": 1,
          "file_action": "",
          "arguments": "wordcount",
          "hql": "",
          "job_state": 2,
          "job_final_status": 0,
          "hive_script_path": "",
          "create_by": "b67132be2f054a45b247365647e05af0",
          "finished_step": 0,
          "job_main_id": "",
          "job_step_id": "",
          "postpone_at": 1496387588,
          "step_name": "",
          "step_num": 0,
          "task_num": 0,
          "update_by": "b67132be2f054a45b247365647e05af0",
          "credentials": "",
          "user_id": "b67132be2f054a45b247365647e05af0",
          "job_configs": null,
          "extra": null,
          "data_source_urls": null,
          "info": null
        }
      }

Status Code
-----------

:ref:`Table 7 <mrs_02_0040__table1584477916050>` describes the status code of this API.

.. _mrs_02_0040__table1584477916050:

.. table:: **Table 7** Status Code

   =========== ====================================
   Status Code Description
   =========== ====================================
   200         The job has been successfully added.
   =========== ====================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
