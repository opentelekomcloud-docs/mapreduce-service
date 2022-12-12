:original_name: mrs_02_0025.html

.. _mrs_02_0025:

Querying the Data Source Details
================================

Function
--------

This API is used to query detailed information about a data source. This API is compatible with Sahara.

URI
---

-  Format

   GET /v1.1/{project_id}/data-sources/{data_source_id}

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

.. table:: **Table 2** Response parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                               |
   +=======================+=======================+===========================================================================================================+
   | is_public             | Bool                  | Whether the data source is public                                                                         |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | tenant_id             | String                | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_protected          | Bool                  | Whether the data source is protected                                                                      |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | created_at            | String                | Data source creation time                                                                                 |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | id                    | String                | Data source ID                                                                                            |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | name                  | String                | Data source name                                                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | updated_at            | String                | Data source update time                                                                                   |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | description           | String                | Data source description                                                                                   |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | url                   | String                | Data source URL                                                                                           |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | type                  | String                | Data source type                                                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   .. code-block:: text

      GET /v1.1/{project_id}/data-sources/{data_source_id}

-  Example response

   .. code-block::

      {
          "data_source": {
              "name": "my-data-source-update",
              "type": "hdfs",
              "url": "/simple/mapreduce/input",
              "description": "this is the data source template",
              "created_at": "2017-06-22T08:28:57",
              "updated_at": "2017-06-22T08:30:08",
              "id": "e275a927-fe72-4b8b-a634-e47a11dca181",
              "tenant_id": "5a3314075bfa49b9ae360f4ecd333695",
              "is_public": false,
              "is_protected": false
          }
      }

Status Code
-----------

:ref:`Table 3 <mrs_02_0025__table1584477916050>` describes the status code of this API.

.. _mrs_02_0025__table1584477916050:

.. table:: **Table 3** Status code

   =========== ===================================================
   Status Code Description
   =========== ===================================================
   200         Data source details have been queried successfully.
   =========== ===================================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
