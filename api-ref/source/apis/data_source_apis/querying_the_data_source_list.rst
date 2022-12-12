:original_name: mrs_02_0024.html

.. _mrs_02_0024:

Querying the Data Source List
=============================

Function
--------

This API is used to query the data source list. This API is compatible with Sahara.

URI
---

-  Format

   GET /v1.1/{project_id}/data-sources

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter             | Mandatory             | Description                                                                                                                                |
      +=======================+=======================+============================================================================================================================================+
      | project_id            | Yes                   | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`.                                  |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
      | limit                 | No                    | Maximum number of objects in response data                                                                                                 |
      |                       |                       |                                                                                                                                            |
      |                       |                       | Value range: 1 to 1073741822                                                                                                               |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
      | marker                | No                    | Data source ID                                                                                                                             |
      |                       |                       |                                                                                                                                            |
      |                       |                       | Query the data source list, and select one data source ID as the marker. The ID is the last element on the list that will not be returned. |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------+
      | sort_by               | No                    | Sort field                                                                                                                                 |
      |                       |                       |                                                                                                                                            |
      |                       |                       | A hyphen (-) before the sort field indicates to sort in descending order. Example:                                                         |
      |                       |                       |                                                                                                                                            |
      |                       |                       | -  **sort_by=name** indicates to sort by name in ascending order.                                                                          |
      |                       |                       | -  **sort_by=-name** indicates to sort by name in descending order.                                                                        |
      +-----------------------+-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

None.

Response
--------

.. table:: **Table 2** Response parameter description

   +--------------+--------+---------------------------------------------------------------------------------------------------------+
   | Parameter    | Type   | Description                                                                                             |
   +==============+========+=========================================================================================================+
   | markers      | Object | Marker object For more parameter description, see :ref:`Table 3 <mrs_02_0024__table35904709104244>`.    |
   +--------------+--------+---------------------------------------------------------------------------------------------------------+
   | data_sources | Array  | Data source list For more parameter description, see :ref:`Table 4 <mrs_02_0024__table53055087104252>`. |
   +--------------+--------+---------------------------------------------------------------------------------------------------------+

.. _mrs_02_0024__table35904709104244:

.. table:: **Table 3** **markers** parameter description

   ========= ====== ===========================
   Parameter Type   Description
   ========= ====== ===========================
   prev      String Marker on the previous page
   next      String Marker on the next page
   ========= ====== ===========================

.. _mrs_02_0024__table53055087104252:

.. table:: **Table 4** **data_sources** parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | Parameter             | Type                  | Description                                                                                               |
   +=======================+=======================+===========================================================================================================+
   | name                  | String                | Data source name                                                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | type                  | String                | Data source type                                                                                          |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | url                   | String                | Data source URL                                                                                           |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | description           | String                | Data source description                                                                                   |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | created_at            | String                | Data source creation time                                                                                 |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | updated_at            | String                | Data source update time                                                                                   |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | id                    | String                | Data source ID                                                                                            |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | tenant_id             | String                | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_public             | Bool                  | Whether the data source is public                                                                         |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+
   | is_protected          | Bool                  | Whether the data source is protected                                                                      |
   |                       |                       |                                                                                                           |
   |                       |                       | -  true                                                                                                   |
   |                       |                       | -  false                                                                                                  |
   |                       |                       |                                                                                                           |
   |                       |                       | The current version does not support this function.                                                       |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   .. code-block:: text

      GET /v1.1/{project_id}/data-sources?sort_by=name&limit=2&marker=81a2d48b-029a-4160-830b-2d0ac51fa3ba

-  Example response

   .. code-block::

      {
          "markers": {
              "prev": "948b92e5-8213-4f5d-975a-435a67c6b93d",
              "next": null
          },
          "data_sources": [
              {
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
              },
              {
                  "name": "my-datasource",
                  "type": "hdfs",
                  "url": "/simple/mapreduce/input",
                  "description": "this is the data source template",
                  "created_at": "2017-06-22T08:22:06",
                  "updated_at": null,
                  "id": "e68164d5-5897-41a7-a550-5de635fffe20",
                  "tenant_id": "5a3314075bfa49b9ae360f4ecd333695",
                  "is_public": false,
                  "is_protected": false
              }
          ]
      }

Status Code
-----------

:ref:`Table 5 <mrs_02_0024__table1584477916050>` describes the status code of this API.

.. _mrs_02_0024__table1584477916050:

.. table:: **Table 5** Status code

   =========== =============================================
   Status Code Description
   =========== =============================================
   200         The data source list is queried successfully.
   =========== =============================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
