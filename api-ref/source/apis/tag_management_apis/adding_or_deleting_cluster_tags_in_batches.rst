:original_name: mrs_02_0074.html

.. _mrs_02_0074:

Adding or Deleting Cluster Tags in Batches
==========================================

Function
--------

This API is used to add or delete tags to or from a specified cluster in batches.

You can add a maximum of 10 tags to a cluster.

This API is idempotent.

-  If a tag to be created has the same key as an existing tag in a cluster, the tag will overwrite the existing one.
-  When tags are being deleted and some tags do not exist, the operation is considered successful by default. The character set of the tags will not be checked. A key and a value can respectively contain up to 36 and 43 Unicode characters. When tags are deleted, the tag structure body cannot be missing, and the key cannot be left blank or set to an empty string.

URI
---

-  Format

   POST /v1.1/{project_id}/clusters/{cluster_id}/tags/action

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

.. table:: **Table 2** Request parameter description

   +-----------+-----------+--------------------+----------------------------------------------------------------------------------------------------+
   | Parameter | Mandatory | Type               | Description                                                                                        |
   +===========+===========+====================+====================================================================================================+
   | action    | Yes       | String             | Operation to be performed. The value can be set to **create** or **delete** only.                  |
   +-----------+-----------+--------------------+----------------------------------------------------------------------------------------------------+
   | tags      | Yes       | List<resource_tag> | Tag list. For details about the parameter, see :ref:`Table 3 <mrs_02_0074__table102451749203418>`. |
   +-----------+-----------+--------------------+----------------------------------------------------------------------------------------------------+

.. _mrs_02_0074__table102451749203418:

.. table:: **Table 3** **tags** parameter description

   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------+
   | Parameter       | Mandatory       | Type            | Description                                                                                                             |
   +=================+=================+=================+=========================================================================================================================+
   | key             | Yes             | String          | Key. A tag key can contain only uppercase letters, lowercase letters, digits, hyphens (-), and underscores (_).         |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------+
   | value           | Yes             | String          | Tag value. A tag value can contain only uppercase letters, lowercase letters, digits, hyphens (-), and underscores (_). |
   |                 |                 |                 |                                                                                                                         |
   |                 |                 |                 | Note:                                                                                                                   |
   |                 |                 |                 |                                                                                                                         |
   |                 |                 |                 | -  This parameter is mandatory for adding a tag.                                                                        |
   |                 |                 |                 | -  This parameter is optional for deleting a tag.                                                                       |
   +-----------------+-----------------+-----------------+-------------------------------------------------------------------------------------------------------------------------+

Response
--------

**Response parameters**

None.

Example
-------

-  Example request

.. code-block::

   {
       "action": "create",
       "tags": [
           {
               "key": "key1",
               "value": "value1"
           },
           {
               "key": "key",
               "value": "value3"
           }
       ]
   }

-  Example response

   None.

Status Code
-----------

:ref:`Table 4 <mrs_02_0074__t8387a0fadf974df1925645625284999c>` describes the status code of this API.

.. _mrs_02_0074__t8387a0fadf974df1925645625284999c:

.. table:: **Table 4** Status code

   =========== ============================
   Status Code Description
   =========== ============================
   204         The operation is successful.
   =========== ============================
