:original_name: mrs_02_0073.html

.. _mrs_02_0073:

Querying Tags of a Specified Cluster
====================================

Function
--------

This API is used to query tags of a specified cluster.

URI
---

-  Format

   GET /v1.1/{project_id}/clusters/{cluster_id}/tags

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

.. table:: **Table 2** Response parameter description

   +-----------+------------------+----------------------------------------------------------------------------+
   | Parameter | Type             | Description                                                                |
   +===========+==================+============================================================================+
   | tags      | Array of objects | Tag list. For details, see :ref:`Table 3 <mrs_02_0073__table16429741613>`. |
   +-----------+------------------+----------------------------------------------------------------------------+

.. _mrs_02_0073__table16429741613:

.. table:: **Table 3** **tags** parameter description

   +-----------+--------+-------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                                                             |
   +===========+========+=========================================================================================================================+
   | key       | String | Key. A tag key can contain only uppercase letters, lowercase letters, digits, hyphens (-), and underscores (_).         |
   +-----------+--------+-------------------------------------------------------------------------------------------------------------------------+
   | value     | String | Tag value. A tag value can contain only uppercase letters, lowercase letters, digits, hyphens (-), and underscores (_). |
   +-----------+--------+-------------------------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   None.

-  Example response

   .. code-block::

      {
             "tags": [
              {
                  "key": "key1",
                  "value": "value1"
              },
              {
                  "key": "key2",
                  "value": "value3"
              }
          ]
      }

Status Code
-----------

:ref:`Table 4 <mrs_02_0073__t8879ab801c3841179c9f683931ddb28e>` describes the status code of this API.

.. _mrs_02_0073__t8879ab801c3841179c9f683931ddb28e:

.. table:: **Table 4** Status code

   =========== ============================
   Status Code Description
   =========== ============================
   200         The operation is successful.
   =========== ============================
