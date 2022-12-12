:original_name: mrs_02_0076.html

.. _mrs_02_0076:

Querying a List of Clusters with Specified Tags
===============================================

Function
--------

This API is used to filter clusters by tag.

By default, clusters and tags are sorted in descending order of creation time.

URI
---

-  Format

   POST /v1.1/{project_id}/clusters/resource_instances/action

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

   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
   +=================+=================+=================+================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+
   | tags            | No              | List<tag>       | The return result contains resources corresponding to all tags in this parameter. This parameter contains a maximum of 10 keys, and each key contains a maximum of 10 values. The structure body cannot be missing, and the key cannot be left blank or set to an empty string.                                                                                                                                                                                                                                                                |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | tags_any        | No              | List<tag>       | The return result contains resources corresponding to any tag in this parameter. This parameter contains a maximum of 10 keys, and each key contains a maximum of 10 values. The structure body cannot be missing, and the key cannot be left blank or set to an empty string. Keys must be unique and values of a key must be unique.                                                                                                                                                                                                         |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | not_tags        | No              | List<tag>       | The return result does not contain resources corresponding to all tags in this parameter. This parameter contains a maximum of 10 keys, and each key contains a maximum of 10 values. The structure body cannot be missing, and the key cannot be left blank or set to an empty string. Keys must be unique and values of a key must be unique.                                                                                                                                                                                                |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | not_tags_any    | No              | List<tag>       | The return result does not contain resources corresponding to any tag in this parameter. This parameter contains a maximum of 10 keys, and each key contains a maximum of 10 values. The structure body cannot be missing, and the key cannot be left blank or set to an empty string. Keys must be unique and values of a key must be unique.                                                                                                                                                                                                 |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | limit           | No              | String          | Number of records. This parameter is not available when **action** is set to **count**. The default value is **1000** when **action** is set to **filter**. The maximum value is **1000**, and the minimum value is **1**. The value cannot be a negative number.                                                                                                                                                                                                                                                                              |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | offset          | No              | String          | Index position. The query starts from the next piece of data specified by the **offset** parameter. This parameter is not required when you query data on the first page. The value in the response body returned for querying data on the previous page will be included in this parameter for querying data on subsequent pages. This parameter is not available when **action** is set to **count**. If **action** is set to **filter**, the value must be a number, and the default value is **0**. The value cannot be a negative number. |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | action          | Yes             | String          | Operation to be performed. The value can be **filter** or **count**.                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                 | The value **filter** indicates pagination query. The value **count** indicates that the total number of query results meeting the search criteria will be returned.                                                                                                                                                                                                                                                                                                                                                                            |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | matches         | No              | List<match>     | Search field. **key** indicates the field to be matched, for example, **resource_name**. **value** indicates the matched value. This field is a fixed dictionary value.                                                                                                                                                                                                                                                                                                                                                                        |
   |                 |                 |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
   |                 |                 |                 | Determine whether fuzzy match is required based on different fields. For example, if **key** is **resource_name**, fuzzy search is used by default. If **value** is an empty string, exact match is used.                                                                                                                                                                                                                                                                                                                                      |
   +-----------------+-----------------+-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 3** **tag** field description

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                                                     |
   +=================+=================+=================+=================================================================================================================================================+
   | key             | Yes             | String          | Key. It contains a maximum of 127 Unicode characters. It cannot be left empty. (This parameter is not verified in the search process.)          |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------+
   | values          | Yes             | List<String>    | List of values. A value contains a maximum of 255 Unicode characters.                                                                           |
   |                 |                 |                 |                                                                                                                                                 |
   |                 |                 |                 | If the values are null, it indicates **any_value**. The relationship between values is OR. By default, only the first value is used for search. |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------+

.. table:: **Table 4** **match** field description

   +-----------+-----------+--------+-----------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type   | Description                                                                       |
   +===========+===========+========+===================================================================================+
   | key       | Yes       | String | Key. The value is fixed to **resource_name**, indicating a cluster name.          |
   +-----------+-----------+--------+-----------------------------------------------------------------------------------+
   | value     | Yes       | String | Value. A value contains a maximum of 64 Unicode characters. Enter a cluster name. |
   +-----------+-----------+--------+-----------------------------------------------------------------------------------+

Response
--------

.. table:: **Table 5** Response parameter description

   +-------------+------------------+-----------------------------------------------------------------------------------+
   | Parameter   | Type             | Description                                                                       |
   +=============+==================+===================================================================================+
   | resources   | Array of objects | Resource details. For details, see :ref:`Table 6 <mrs_02_0076__table5936005416>`. |
   +-------------+------------------+-----------------------------------------------------------------------------------+
   | total_count | Integer          | Total number of resources.                                                        |
   +-------------+------------------+-----------------------------------------------------------------------------------+

.. _mrs_02_0076__table5936005416:

.. table:: **Table 6** **resources** parameters

   +-----------------+---------+------------------------------------------------------------------------------+
   | Parameter       | Type    | Description                                                                  |
   +=================+=========+==============================================================================+
   | resource_detail | String  | Resource details.                                                            |
   +-----------------+---------+------------------------------------------------------------------------------+
   | resource_id     | String  | Resource ID.                                                                 |
   +-----------------+---------+------------------------------------------------------------------------------+
   | resource_name   | String  | Resource name.                                                               |
   +-----------------+---------+------------------------------------------------------------------------------+
   | tags            | objects | Tag list. For details, see :ref:`Table 7 <mrs_02_0076__table1897413881916>`. |
   +-----------------+---------+------------------------------------------------------------------------------+

.. _mrs_02_0076__table1897413881916:

.. table:: **Table 7** **tags** parameter description

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

   Request body when **action** is set to **filter**

   .. code-block::

      {
        "offset": "100",
        "limit": "100",
      "action": "filter",
        "matches":[
      {
              "key": "resource_name",
              "value": "clusterA"
             }
      ],
         "not_tags": [
          {
            "key": "key1",
            "values": [
              "value1",
              "value2"
            ]
          }
        ],
        "tags": [
          {
            "key": "key1",
            "values": [
              "value1",
              "value2"
            ]
          }
        ],
        "tags_any": [
          {
            "key": "key1",
            "values": [
              "value1",
              "value2"
            ]
          }
        ],
      "not_tags_any": [
          {
            "key": "key1",
            "values": [
              "value1",
              "value2"
            ]
          }
        ]
      }

   Request body when **action** is set to **count**

   .. code-block::

      {
        "action": "count",
        "not_tags": [
          {
            "key": "key1",
            "values": [
              "value1",
              "value2"
            ]
          }
        ],
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
        ],
        "tags_any": [
          {
            "key": "key1",
            "values": [
              "value1",
              "value2"
            ]
          }
        ],
      "not_tags_any": [
          {
            "key": "key1",
            "values": [
              "value1",
              "value2"
            ]
          }
         ],
      "matches":[
      {
              "key": "resource_name",
              "value": "clusterA"
             }
      ]
      }

-  Example response

   Response body when **action** is set to **filter**

   .. code-block::

          {
            "resources": [
               {
                  "resource_detail": null,
                  "resource_id": "cdfs_cefs_wesas_12_dsad",
                  "resource_name": "clusterA"
               }
             ]
            "total_count": 1000
      }

   Response body when **action** is set to **count**

   .. code-block::

      {
             "total_count": 1000
      }

Status Code
-----------

:ref:`Table 8 <mrs_02_0076__t31bfd33136f84cd88b311dc479046586>` describes the status code of this API.

.. _mrs_02_0076__t31bfd33136f84cd88b311dc479046586:

.. table:: **Table 8** Status code

   =========== ============================
   Status Code Description
   =========== ============================
   200         The operation is successful.
   =========== ============================
