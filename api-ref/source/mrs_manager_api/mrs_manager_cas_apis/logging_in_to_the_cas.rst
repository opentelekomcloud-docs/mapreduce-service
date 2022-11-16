:original_name: mrs_02_1084.html

.. _mrs_02_1084:

Logging In to the CAS
=====================

Function
--------

This API is used to submit a CAS login request. This API can be used only by security clusters that support Kerberos authentication.

URI
---

POST /cas/login

Request
-------

-  Example:

.. code-block:: text

   POST /cas/login HTTP/1.1
   Host: example.com
   Content-Type: application/json
   Accept:application/json
   username: String
   password: String
   lt: String
   _eventId: String
   Submit: String

-  Parameter description

+-----------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Parameter | Mandatory or Not | Description                                                                                                                                                                                                       |
+===========+==================+===================================================================================================================================================================================================================+
| username  | Yes              | User name                                                                                                                                                                                                         |
+-----------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| password  | Yes              | Password                                                                                                                                                                                                          |
+-----------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| lt        | Yes              | Login ticket. Follow instructions in step 1 in the **Obtaining Request Authentication Information** part of the section :ref:`API Calling Process <mrs_02_1080>` to send a GET request to obtain **loginTicket**. |
+-----------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| \_eventId | Yes              | Event type. The default value is **submit**.                                                                                                                                                                      |
+-----------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| submit    | Yes              | Submission type. The default value is **Login**.                                                                                                                                                                  |
+-----------+------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Response
--------

-  Example

   .. code-block::

      HTTP/1.1 200 OK
      Data:Wed,02 May 2018 10:10:01 GMT
      Server: example-server
      Content-Type: application/json

-  Parameter description

   None

Status Code
-----------

.. table:: **Table 1** Status code

   =========== ========================
   Status Code Description
   =========== ========================
   200         The login is successful.
   =========== ========================

For details about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
