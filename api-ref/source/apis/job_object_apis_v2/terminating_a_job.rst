:original_name: mrs_02_0088.html

.. _mrs_02_0088:

Terminating a Job
=================

Function
--------

This API is used to terminate a specified job in an MRS cluster.

URI
---

-  Format

   POST /v2/{project_id}/clusters/{cluster_id}/job-executions/{job_execution_id}/kill

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

**Response parameters**

None

Example
-------

-  Example request

   None

-  Example response

   -  Example of a successful response

      None

   -  Example of a failed response

      .. code-block::

         {
         "error_msg": "Failed to terminate the job."
         "error_code":"0175"
         }

Status Code
-----------

:ref:`Table 2 <mrs_02_0088__table1584477916050>` describes status codes.

.. _mrs_02_0088__table1584477916050:

.. table:: **Table 2** Status code

   =========== ===========================================================
   Status Code Description
   =========== ===========================================================
   202         The job termination request has been accepted. Please wait.
   =========== ===========================================================

For details about status codes, see :ref:`Status Codes <mrs_02_0015>`.
