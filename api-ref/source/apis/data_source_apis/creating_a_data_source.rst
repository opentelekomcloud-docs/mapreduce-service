:original_name: mrs_02_0022.html

.. _mrs_02_0022:

Creating a Data Source
======================

Function
--------

This API is used to create a data source. This API is compatible with Sahara.

URI
---

-  Format

   POST /v1.1/{project_id}/data-sources

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Parameter  | Mandatory | Description                                                                                               |
      +============+===========+===========================================================================================================+
      | project_id | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +------------+-----------+-----------------------------------------------------------------------------------------------------------+

Request
-------

.. table:: **Table 2** Request parameter description

   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                         |
   +=================+=================+=================+=====================================================================================================+
   | name            | Yes             | String          | Data source name                                                                                    |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | Contains 1 to 80 characters and consists of letters, digits, hyphens (-), and underscores (_) only. |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | url             | Yes             | String          | Data source URL                                                                                     |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | Contains 1 to 255 characters.                                                                       |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | -  If the data source type is HDFS, the value is **/**\ *Save path of the data source*.             |
   |                 |                 |                 | -  If the data source type is OBS, the value is **s3a://**\ *Save path of the data source*.         |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | credentials     | No              | Object          | Authentication information. The current version does not support this function.                     |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | is_protected    | No              | Bool            | Whether the data source is protected                                                                |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | -  true                                                                                             |
   |                 |                 |                 | -  false                                                                                            |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | The current version does not support this function.                                                 |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | is_public       | No              | Bool            | Whether the data source is public                                                                   |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | -  true                                                                                             |
   |                 |                 |                 | -  false                                                                                            |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | The current version does not support this function.                                                 |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | type            | Yes             | String          | Data source type                                                                                    |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | -  hdfs                                                                                             |
   |                 |                 |                 | -  obs                                                                                              |
   |                 |                 |                 | -  swift (not supported by the current version)                                                     |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+
   | description     | No              | String          | Data source description                                                                             |
   |                 |                 |                 |                                                                                                     |
   |                 |                 |                 | Contains a maximum of 65535 characters.                                                             |
   +-----------------+-----------------+-----------------+-----------------------------------------------------------------------------------------------------+

Response
--------

.. table:: **Table 3** Response parameter description

   +--------------+--------+-----------------------------------------------------------------------------------------------------------+
   | Parameter    | Type   | Description                                                                                               |
   +==============+========+===========================================================================================================+
   | description  | String | Data source description                                                                                   |
   +--------------+--------+-----------------------------------------------------------------------------------------------------------+
   | url          | String | Data source URL                                                                                           |
   +--------------+--------+-----------------------------------------------------------------------------------------------------------+
   | tenant_id    | String | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
   +--------------+--------+-----------------------------------------------------------------------------------------------------------+
   | created_at   | String | Data source creation time                                                                                 |
   +--------------+--------+-----------------------------------------------------------------------------------------------------------+
   | updated_at   | String | Data source update time If the data source has not been updated, the value of this parameter is **null**. |
   +--------------+--------+-----------------------------------------------------------------------------------------------------------+
   | is_protected | Bool   | Whether the data source is protected                                                                      |
   +--------------+--------+-----------------------------------------------------------------------------------------------------------+
   | is_public    | Bool   | Whether the data source is public                                                                         |
   +--------------+--------+-----------------------------------------------------------------------------------------------------------+
   | type         | String | Data source type                                                                                          |
   +--------------+--------+-----------------------------------------------------------------------------------------------------------+
   | id           | String | ID returned by the system after the data source is created                                                |
   +--------------+--------+-----------------------------------------------------------------------------------------------------------+
   | name         | String | Data source name                                                                                          |
   +--------------+--------+-----------------------------------------------------------------------------------------------------------+

Example
-------

-  Example request

   .. code-block::

      {
          "name": "my-data-source",
          "url": "/simple/mapreduce/input",
          "is_protected": false,
          "is_public": false,
          "type": "hdfs",
          "description": "this is the data source template"
      }

-  Example response

   .. code-block::

      {
          "data_source": {
              "name": "my-data-source",
              "type": "hdfs",
              "url": "/simple/mapreduce/input",
              "description": "this is the data source template",
              "created_at": "2017-06-22T08:28:57",
              "updated_at": null,
              "id": "e275a927-fe72-4b8b-a634-e47a11dca181",
              "tenant_id": "5a3314075bfa49b9ae360f4ecd333695",
              "is_public": false,
              "is_protected": false
          }
      }

Status Code
-----------

:ref:`Table 4 <mrs_02_0022__table1584477916050>` describes the status code of this API.

.. _mrs_02_0022__table1584477916050:

.. table:: **Table 4** Status code

   =========== ==============================================
   Status Code Description
   =========== ==============================================
   202         The data source has been successfully created.
   =========== ==============================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
