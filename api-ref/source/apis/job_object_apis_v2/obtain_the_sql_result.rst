:original_name: mrs_02_0090.html

.. _mrs_02_0090:

Obtain the SQL Result
=====================

Function
--------

This API is used to obtain results returned after the SQL statements for querying SparkSQL and SparkScript jobs in an MRS cluster are executed.

URI
---

-  Format

   GET /v2/{project_id}/clusters/{cluster_id}/job-executions/{job_execution_id}/sql-result

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

None

Response
--------

.. table:: **Table 2** Response parameter description

   =========== ====== ===========================
   Parameter   Type   Description
   =========== ====== ===========================
   sql-results Object SQL statement query result.
   =========== ====== ===========================

Example
-------

-  Example request

   .. code-block::

      {
          "job_name": "111",
          "job_type": "SparkSql",
          "arguments": [
                   "create table src_wordcount (id int,name string);
                    show tables;
                    insert INTO src_wordcount VALUES (1, 'a');
                    insert INTO src_wordcount VALUES (2, 'b');SELECT * FROM src_wordcount;"
                        ],
          "properties": {}
      }

-  Example response

   -  Example of a successful response

      .. code-block::

         {
             "sql_results": {
                 "0": [{
                     "result": "succeed"
                 }],
                 "1": [{
                     "database": "default",
                     "isTemporary": "false",
                     "tableName": "src_wordcount"
                 }],
                 "2": [{
                     "result": "succeed"
                 }],
                 "3": [{
                     "result": "succeed"
                 }],
                 "4": [{
                     "name": "a",
                     "id": "1"
                 }, {
                     "name": "b",
                     "id": "2"
                 }]
             }
         }

   -  Example of a failed response

      .. code-block::

         {
         "error_msg": "Failed to collect SQL job results."
         "error_code":"0172"
         }

Status Code
-----------

For details about status codes, see :ref:`Status Codes <mrs_02_0015>`.
