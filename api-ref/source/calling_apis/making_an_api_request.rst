:original_name: mrs_02_0008.html

.. _mrs_02_0008:

Making an API Request
=====================

This section describes the structure of a REST API, and uses the IAM API for `obtaining request authentication <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__ as an example to demonstrate how to call an API. The obtained token is used to authenticate the calling of other APIs.

Request URI
-----------

A request URI is in the following format:

**{URI-scheme}://{Endpoint}/{resource-path}?{query-string}**

Although a request URI is included in the request header, most programming languages or frameworks require the request URI to be transmitted separately.

.. table:: **Table 1** URI parameter description

   +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter     | Description                                                                                                                                                                                                                                                                                    |
   +===============+================================================================================================================================================================================================================================================================================================+
   | URI-scheme    | Protocol used to transmit requests. All APIs use HTTPS.                                                                                                                                                                                                                                        |
   +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Endpoint      | Domain name or IP address of the server bearing the REST service. The endpoint varies between services in different regions. It can be obtained from `Regions and Endpoints <https://docs.otc.t-systems.com/en-us/endpoint/index.html>`__.                                                     |
   +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource-path | Access path of an API for performing a specified operation. Obtain the path from the URI of an API. For example, the **resource-path** of the API used to `obtain request authentication <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__ is **/v3/auth/tokens**. |
   +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | query-string  | Query parameter, which is optional. Ensure that a question mark (?) is included before each query parameter that is in the format of "*Parameter name=Parameter value*". For example, **? limit=10** indicates that a maximum of 10 data records will be displayed.                            |
   +---------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

.. note::

   To simplify the URI display in this document, each API is provided only with a **resource-path** and a request method. The **URI-scheme** of all APIs is **HTTPS**, and the endpoints of all APIs in the same region are identical.

Request Methods
---------------

The HTTP protocol defines the following request methods that can be used to send a request to the server:

.. table:: **Table 2** HTTP methods

   +-----------------------------------+----------------------------------------------------------------------------+
   | Method                            | Description                                                                |
   +===================================+============================================================================+
   | GET                               | Requests the server to return specified resources.                         |
   +-----------------------------------+----------------------------------------------------------------------------+
   | PUT                               | Requests the server to update specified resources.                         |
   +-----------------------------------+----------------------------------------------------------------------------+
   | POST                              | Requests the server to add resources or perform special operations.        |
   +-----------------------------------+----------------------------------------------------------------------------+
   | DELETE                            | Requests the server to delete specified resources, for example, an object. |
   +-----------------------------------+----------------------------------------------------------------------------+
   | HEAD                              | Same as GET except that the server must return only the response header.   |
   +-----------------------------------+----------------------------------------------------------------------------+
   | PATCH                             | Requests the server to update partial content of a specified resource.     |
   |                                   |                                                                            |
   |                                   | If the resource does not exist, a new resource will be created.            |
   +-----------------------------------+----------------------------------------------------------------------------+

In the URI of the API to `obtain request authentication <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__, you can see that the request method is **POST**. The request is as follows:

.. code-block:: text

   POST https://{{endpoint}}/v3/auth/tokens

Request Header
--------------

You can also add additional header fields to a request, such as the fields required by a specified URI or HTTP method. For example, to request for the authentication information, add **Content-Type**, which specifies the request body type.

:ref:`Table 3 <mrs_02_0008__td181b06f1c0949cb913acd8d77f21ec3>` lists common request header fields.

.. _mrs_02_0008__td181b06f1c0949cb913acd8d77f21ec3:

.. table:: **Table 3** Common request header fields

   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------------+
   | Field           | Description                                                                                                                                                                                                                                                 | Mandatory                                                                                   | Example                          |
   +=================+=============================================================================================================================================================================================================================================================+=============================================================================================+==================================+
   | X-Sdk-Date      | Time when the request is sent. The time is in **YYYYMMDD'T'HHMMSS'Z'** format.                                                                                                                                                                              | This field is mandatory for AK/SK-based authentication.                                     | 20150907T101459Z                 |
   |                 |                                                                                                                                                                                                                                                             |                                                                                             |                                  |
   |                 | The value is the current Greenwich Mean Time (GMT) of the system.                                                                                                                                                                                           |                                                                                             |                                  |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------------+
   | Host            | Server information of the resource being requested. The value can be obtained from the URL of a service API. The value is **hostname[:port]**. If the port number is not specified, the default port is used. The default port number for HTTPS is **443**. | This field is mandatory for AK/SK-based authentication.                                     | code.test.com                    |
   |                 |                                                                                                                                                                                                                                                             |                                                                                             |                                  |
   |                 |                                                                                                                                                                                                                                                             |                                                                                             | or                               |
   |                 |                                                                                                                                                                                                                                                             |                                                                                             |                                  |
   |                 |                                                                                                                                                                                                                                                             |                                                                                             | code.test.com:443                |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------------+
   | Content-Type    | MIME type of the request body This field is mandatory and its default value is **application/json**. Other values of this field will be provided for specific APIs if any.                                                                                  | Yes                                                                                         | application/json                 |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------------+
   | Content-Length  | Length of the request body. The unit is byte.                                                                                                                                                                                                               | This field is mandatory for POST and PUT requests, but must be left blank for GET requests. | 3495                             |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------------+
   | X-Project-Id    | Project ID. This field is used to obtain the token for each project.                                                                                                                                                                                        | No                                                                                          | e9993fc787d94b6c886cbaa340f9c0f4 |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------------+
   | X-Auth-Token    | User token.                                                                                                                                                                                                                                                 | No                                                                                          | ``-``                            |
   |                 |                                                                                                                                                                                                                                                             |                                                                                             |                                  |
   |                 | It is the response to the API used to `obtain request authentication <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__. This API is the only one that does not require authentication.                                          | This field is mandatory for token-based authentication.                                     |                                  |
   |                 |                                                                                                                                                                                                                                                             |                                                                                             |                                  |
   |                 | The token is the value of **X-Subject-Token** in the response header.                                                                                                                                                                                       |                                                                                             |                                  |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------------+
   | X-Language      | Request language. The options are as follows:                                                                                                                                                                                                               | No                                                                                          | en-us                            |
   |                 |                                                                                                                                                                                                                                                             |                                                                                             |                                  |
   |                 | **en-us**: English                                                                                                                                                                                                                                          |                                                                                             |                                  |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------------+
   | X-Domain-Id     | Domain ID                                                                                                                                                                                                                                                   | No                                                                                          | ``-``                            |
   +-----------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------------------+----------------------------------+

.. note::

   In addition to supporting token-based authentication, APIs also support authentication using access key ID/secret access key (AK/SK). During AK/SK-based authentication, an SDK is used to sign the request, and the **Authorization** (signature authentication) and **X-Sdk-Date** (time when the request is sent) header fields are automatically added to the request.

   For more information, see **AK/SK-based Authentication** in :ref:`Authentication <mrs_02_0009>`.

The API used to `obtain a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__ does not require authentication. Therefore, only the **Content-Type** field needs to be added to requests for calling the API. An example of such requests is as follows:

.. code-block:: text

   POST https://{{endpoint}}/v3/auth/tokens
   Content-Type: application/json

(Optional) Request Body
-----------------------

This part is optional. The body of a request is often sent in a structured format (for example, JSON or XML) as specified in the **Content-Type** header field. The request body transfers content except the request header.

The request body varies between APIs. Some APIs do not require the request body, such as the APIs requested using the GET and DELETE methods.

In the case of the API used to `obtain a user token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__, the request parameters and parameter description can be obtained from the API request. The following provides an example request with a body included. Replace *username*, *domainname*, ``********`` (login password), and *xxxxxxxxxxxxxxxxxx* *(project ID)* with the actual values. To learn how to obtain a project ID, see :ref:`Obtaining a Project ID <mrs_02_0011>`.

.. note::

   The **scope** parameter specifies where a token takes effect. You can set **scope** to an account or a project under an account. In the following example, the token takes effect only for the resources in a specified project. For more information about this API, see `Obtaining a User Token <https://docs.otc.t-systems.com/en-us/api/iam/en-us_topic_0057845583.html>`__ of the IAM service.

.. code-block:: text

   POST https://{{endpoint}}/v3/auth/tokens
   Content-Type: application/json

   {
       "auth": {
           "identity": {
               "methods": [
                   "password"
               ],
               "password": {
                   "user": {
                       "name": "username",
                       "password": "********",
                       "domain": {
                           "name": "domainname"
                       }
                   }
               }
           },
           "scope": {
               "project": {
                   "id": "xxxxxxxxxxxxxxxxxx"
               }
           }
       }
   }

If all data required for the API request is available, you can send the request to call the API through `curl <https://curl.haxx.se/>`__, `Postman <https://www.getpostman.com/>`__, or coding. In the response to the API used to obtain a user token, **x-subject-token** is the desired user token. This token can then be used to authenticate the calling of other APIs.
