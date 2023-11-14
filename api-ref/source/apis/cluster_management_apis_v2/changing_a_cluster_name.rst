:original_name: mrs_02_0201.html

.. _mrs_02_0201:

Changing a Cluster Name
=======================

Function
--------

This API is used to change a cluster name.

URI
---

PUT /v2/{project_id}/clusters/{cluster_id}/cluster-name

.. table:: **Table 1** URI parameters

   +------------+-----------+--------+------------------------------------------------------------------------------------------------------------------+
   | Parameter  | Mandatory | Type   | Description                                                                                                      |
   +============+===========+========+==================================================================================================================+
   | project_id | Yes       | String | The project ID. For details about how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +------------+-----------+--------+------------------------------------------------------------------------------------------------------------------+
   | cluster_id | Yes       | String | The cluster ID. For details about how to obtain the cluster ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +------------+-----------+--------+------------------------------------------------------------------------------------------------------------------+

Request Parameters
------------------

.. table:: **Table 2** Request body parameter

   ============ ========= ====== =====================
   Parameter    Mandatory Type   Description
   ============ ========= ====== =====================
   cluster_name Yes       String The new cluster name.
   ============ ========= ====== =====================

Response Parameters
-------------------

**Status code: 200**

.. table:: **Table 3** Response body parameter

   +-----------+--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                                                                                                                      |
   +===========+========+==================================================================================================================================================================================+
   | result    | String | The operation result of the mapping update request. Value \**succeeded*\* indicates that the operation is successful, and value \**failed*\* indicates that the operation fails. |
   +-----------+--------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

**Status code: 400**

.. table:: **Table 4** Response body parameters

   ========== ====== ==================
   Parameter  Type   Description
   ========== ====== ==================
   error_code String The error code.
   error_msg  String The error message.
   ========== ====== ==================

Example Request
---------------

Change the MRS cluster name to **mrs_jdRU_dm01**.

.. code-block::

   {
     "cluster_name" : "mrs_jdRU_dm01"
   }

Example Response
----------------

**Status code: 200**

The cluster name is changed.

.. code-block::

   {
     "result" : "succeeded"
   }

Status Codes
------------

See :ref:`Status Codes <mrs_02_0015>`.

Error Codes
-----------

See :ref:`Error Code <mrs_02_0014>`.
