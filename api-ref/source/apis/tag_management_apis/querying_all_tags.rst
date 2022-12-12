:original_name: mrs_02_0075.html

.. _mrs_02_0075:

Querying All Tags
=================

Function
--------

This API is used to query all tag sets of a specified region.

URI
---

-  Format

   GET /v1.1/{project_id}/clusters/tags

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Parameter  | Mandatory | Description                                                                                               |
      +============+===========+===========================================================================================================+
      | project_id | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
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
   | tags      | Array of objects | Tag list. For details, see :ref:`Table 3 <mrs_02_0075__table45211674182>`. |
   +-----------+------------------+----------------------------------------------------------------------------+

.. _mrs_02_0075__table45211674182:

.. table:: **Table 3** **tags** parameter description

   +-----------+--------+-------------------------------------------------------------------------------------------------------------------------+
   | Parameter | Type   | Description                                                                                                             |
   +===========+========+=========================================================================================================================+
   | key       | String | Tag key. A tag key can contain only uppercase letters, lowercase letters, digits, hyphens (-), and underscores (_).     |
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
           "values": [
               "value1",
               "value2"
           ]
           },
           {
           "key": "key2",
           "values": [
               "value1",
               "value2"
           ]
           }
       ]
   }

Status Code
-----------

:ref:`Table 4 <mrs_02_0075__tb472a78155014ba18b372672dd8358e7>` describes the status code of this API.

.. _mrs_02_0075__tb472a78155014ba18b372672dd8358e7:

.. table:: **Table 4** Status code

   =========== ============================
   Status Code Description
   =========== ============================
   200         The operation is successful.
   =========== ============================
