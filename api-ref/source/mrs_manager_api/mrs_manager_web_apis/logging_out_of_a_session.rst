:original_name: mrs_02_1093.html

.. _mrs_02_1093:

Logging Out Of a Session
========================

Function
--------

This API is used to return a temporary redirection, that is, a URL for logging out of the CAS, when you log out of the MapReduce Service system. This API can be used only by security clusters that support Kerberos authentication.

URI
---

-  Format

GET /web/v1/logout_action

-  Parameter description

.. table:: **Table 1** URI parameter description

   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter             | Mandatory or Not      | Description                                                                                                                                                                 |
   +=======================+=======================+=============================================================================================================================================================================+
   | is_timeout_logout     | No                    | Whether to exit due to page timeout. This parameter is optional. Different audit logs are recorded in the background when a user logs out manually or exits due to timeout. |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | Possible values are as follows:                                                                                                                                             |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **true**: Logout due to timeout                                                                                                                                             |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | **false**: Manual logout                                                                                                                                                    |
   |                       |                       |                                                                                                                                                                             |
   |                       |                       | The default value is **false**.                                                                                                                                             |
   +-----------------------+-----------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Request
-------

-  Example:

   .. code-block:: text

      GET /web/v1/logout_action?is_timeout_logout=null HTTP/1.1
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

=========== ============================
Status Code Description
=========== ============================
200         The operation is successful.
=========== ============================

For details about error status codes, see :ref:`Status Codes <mrs_02_0015>`.
