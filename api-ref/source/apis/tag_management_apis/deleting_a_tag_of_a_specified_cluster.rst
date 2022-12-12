:original_name: mrs_02_0072.html

.. _mrs_02_0072:

Deleting a Tag of a Specified Cluster
=====================================

Function
--------

This API is used to delete a tag of a specified cluster.

URI
---

-  Format

   DELETE /v1.1/{project_id}/clusters/{cluster_id}/tags/{key}

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

None

Example
-------

-  Example request

   None.

-  Example response

   None

Status Code
-----------

:ref:`Table 2 <mrs_02_0072__t72c4159e310d449696ec7ba265e3428e>` describes the status code of this API.

.. _mrs_02_0072__t72c4159e310d449696ec7ba265e3428e:

.. table:: **Table 2** Status code

   =========== ============================
   Status Code Description
   =========== ============================
   204         The operation is successful.
   =========== ============================
