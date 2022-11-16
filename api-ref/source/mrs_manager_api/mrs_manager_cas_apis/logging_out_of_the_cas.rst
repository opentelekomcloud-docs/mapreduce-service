:original_name: mrs_02_1085.html

.. _mrs_02_1085:

Logging Out of the CAS
======================

Function
--------

This API is used to destruct the CAS single sign-on (SSO) session of a client. This API can be used only by security clusters that support Kerberos authentication.

URI
---

POST /cas/logout

Request
-------

-  Example:

   .. code-block:: text

      POST /cas/logout HTTP/1.1
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

-  Parameter description

   None

Status Code
-----------

=========== =========================
Status Code Description
=========== =========================
200         The logout is successful.
=========== =========================

For details about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
