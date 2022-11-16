:original_name: mrs_02_0032.html

.. _mrs_02_0032:

Deleting a Cluster
==================

Function
--------

This API is used to delete a cluster after data processing and analysis are completed or the cluster is abnormal. This API is compatible with Sahara.

Clusters in any of the following states cannot be terminated:

-  scaling-out
-  scaling-in
-  starting
-  terminating
-  terminated
-  failed

URI
---

-  Format

   DELETE /v1.1/{project_id}/clusters/{cluster_id}

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Parameter  | Mandatory | Description                                                                                               |
      +============+===========+===========================================================================================================+
      | project_id | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | cluster_id | Yes       | Cluster ID                                                                                                |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

None.

Response
--------

**Response parameters**

None.

Example
-------

-  Example request

   None.

-  Example response

   None.

Status Code
-----------

:ref:`Table 2 <mrs_02_0032__table1584477916050>` describes the status code of this API.

.. _mrs_02_0032__table1584477916050:

.. table:: **Table 2** Status code

   =========== =============================================
   Status Code Description
   =========== =============================================
   204         The cluster has been successfully terminated.
   =========== =============================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
