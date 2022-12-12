:original_name: mrs_02_0026.html

.. _mrs_02_0026:

Deleting a Data Source
======================

Function
--------

This API is used to delete a data source. This API is compatible with Sahara.

URI
---

-  Format

   DELETE /v1.1/{project_id}/data-sources/{data_source_id}

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +----------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Parameter      | Mandatory | Description                                                                                               |
      +================+===========+===========================================================================================================+
      | project_id     | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +----------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | data_source_id | Yes       | Data source ID                                                                                            |
      +----------------+-----------+-----------------------------------------------------------------------------------------------------------+

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

   .. code-block:: text

      DELETE /v1.1/{project_id}/data-sources/{data_source_id}

-  Example response

   None.

Status Code
-----------

:ref:`Table 2 <mrs_02_0026__table1584477916050>` describes the status code of this API.

.. _mrs_02_0026__table1584477916050:

.. table:: **Table 2** Status code

   =========== ========================================
   Status Code Description
   =========== ========================================
   204         The data source is deleted successfully.
   =========== ========================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
