:original_name: mrs_02_0089.html

.. _mrs_02_0089:

Deleting Jobs in Batches
========================

Function
--------

This API is used to delete APIs in batches.

URI
---

-  Format

   POST /v2/{project_id}/clusters/{cluster_id}/job-executions/batch-delete

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

   +-------------+-----------+-------+--------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter   | Mandatory | Type  | Description                                                                                                                          |
   +=============+===========+=======+======================================================================================================================================+
   | job_id_list | Yes       | Array | List of job IDs. For details on how to obtain the list of job IDs, see :ref:`Obtaining a Job ID <mrs_02_0091__section247234143612>`. |
   +-------------+-----------+-------+--------------------------------------------------------------------------------------------------------------------------------------+

Response
--------

**Response parameters**

None

Example
-------

-  Example request

   .. code-block::

      {
          "job_id_list": ["c23c1f53-5c8e-4eb8-ab2f-a6acff8ac369", "8f7969b6-d2fb-4442-9533-3fe7d7bdf31b"]
      }

-  Example response

   -  Example of a successful response

      None

   -  Example of a failed response

      .. code-block::

         {
         "error_msg": "Failed to delete jobs in batches.",
         "error_code":"0161"
         }

Status Code
-----------

For details about status codes, see :ref:`Status Codes <mrs_02_0015>`.
