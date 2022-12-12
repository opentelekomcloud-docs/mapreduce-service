:original_name: mrs_02_0071.html

.. _mrs_02_0071:

Adding a Tag to a Specified Cluster
===================================

Function
--------

This API is used to add a tag to a specified cluster.

A cluster has a maximum of 10 tags. This API is idempotent. If a tag to be created has the same key as an existing tag, the tag will overwrite the existing one.

URI
---

-  Format

   POST /v1.1/{project_id}/clusters/{cluster_id}/tags

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

.. table:: **Table 2** **tags** parameter description

   +-----------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type   | Description                                                                                                             |
   +===========+===========+========+=========================================================================================================================+
   | key       | Yes       | String | Key. A tag key can contain only uppercase letters, lowercase letters, digits, hyphens (-), and underscores (_).         |
   +-----------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------+
   | value     | Yes       | String | Tag value. A tag value can contain only uppercase letters, lowercase letters, digits, hyphens (-), and underscores (_). |
   +-----------+-----------+--------+-------------------------------------------------------------------------------------------------------------------------+

Response
--------

**Response parameters**

None.

Example
-------

-  Example request

.. code-block::

   {
       "tag":
           {
               "key":"DEV",
               "value":"DEV1"
           }
   }

-  Example response

   None.

Status Code
-----------

:ref:`Table 3 <mrs_02_0071__t853eb843894541af90b6f0a45bbc833f>` describes the status code of this API.

.. _mrs_02_0071__t853eb843894541af90b6f0a45bbc833f:

.. table:: **Table 3** Status code

   =========== ============================
   Status Code Description
   =========== ============================
   204         The operation is successful.
   =========== ============================
