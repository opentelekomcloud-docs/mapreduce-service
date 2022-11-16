:original_name: mrs_02_0038.html

.. _mrs_02_0038:

Deleting a Job Binary Object
============================

Function
--------

This API is used to delete a binary object. This API is compatible with Sahara.

URI
---

-  Format

   DELETE /v1.1/{project_id}/job-binaries/{job_binary_id}

-  Parameter description

   .. table:: **Table 1** URI parameter description

      +---------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | Parameter     | Mandatory | Description                                                                                               |
      +===============+===========+===========================================================================================================+
      | project_id    | Yes       | Project ID. For details on how to obtain the project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`. |
      +---------------+-----------+-----------------------------------------------------------------------------------------------------------+
      | job_binary_id | Yes       | Job binary object ID                                                                                      |
      +---------------+-----------+-----------------------------------------------------------------------------------------------------------+

Request
-------

**Request parameters**

None

Response
--------

**Response parameters**

None

Example
-------

-  Example request

   None

-  Example response

   None

Status Code
-----------

:ref:`Table 2 <mrs_02_0038__table1584477916050>` describes the status code of this API.

.. _mrs_02_0038__table1584477916050:

.. table:: **Table 2** Status code

   =========== ==========================================
   Status code Description
   =========== ==========================================
   204         The binary object is deleted successfully.
   =========== ==========================================

For the description about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
