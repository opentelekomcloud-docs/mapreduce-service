:original_name: mrs_02_1088.html

.. _mrs_02_1088:

Modifying the Password of the Current Login User
================================================

Function
--------

This API is used to change the password of the current login user. This API can be used only by security clusters that support Kerberos authentication.

URI
---

-  Format

POST /web/v1/access/modify_self_password

-  Parameter description

================ ================ ================
Parameter        Mandatory or Not Description
================ ================ ================
old_password     Yes              Old password
new_password     Yes              New password
confirm_password Yes              Confirm password
================ ================ ================

Request
-------

-  Example:

   .. code-block:: text

      POST /web/v1/access/modify_self_password?old_password=null&new_password=null& confirm_password=null HTTP/1.1
      Host: example.com
      Content-Type: application/json
      Accept:application/json

-  Parameter description

   None

Response
--------

-  Example:

   .. code-block::

      HTTP/1.1 200 OK
      Data:Wed,02 May 2018 10:10:01 GMT
      Server: example-server
      Content-Type: application/json
      {
        "int_result_code": 0,
        "result_desc": "string"
      }

-  Parameter description

+-----------------+------------------+---------+----------------------------------+
| Parameter       | Mandatory or Not | Type    | Description                      |
+=================+==================+=========+==================================+
| int_result_code | No               | INTEGER | Code of the return result        |
+-----------------+------------------+---------+----------------------------------+
| result_desc     | No               | STRING  | Description of the return result |
+-----------------+------------------+---------+----------------------------------+

Status Code
-----------

=========== ============================
Status Code Description
=========== ============================
200         The operation is successful.
=========== ============================

For details about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
