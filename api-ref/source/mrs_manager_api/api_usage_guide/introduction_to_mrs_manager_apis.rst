:original_name: mrs_02_1019.html

.. _mrs_02_1019:

Introduction to MRS Manager APIs
================================

MRS Manager APIs are provided for you to query basic information about MRS clusters and monitoring status, as well as start and stop services.

MRS Manager APIs can be accessed by only nodes in the same VPC as the cluster.

Clusters with Kerberos authentication disabled can directly call MRS Manager APIs in the same VPC for access. However, clusters with Kerberos authentication enabled must obtain authentication information before calling MRS Manager APIs.

An MRS Manager API request/response consists of the following six parts:

-  Request URI
-  Request mode
-  Request header
-  Request body
-  Response header
-  Response body

Request URI
-----------

A request URI is in the following format:

**{URI-scheme} :// {MRS Manager floating IP address} :{MRS Manager port}/ {resource-path} ? {query-string}**

Although the request URI is included in the request header, most languages or frameworks require that it be transmitted separately from the request message. Therefore, the request URI is listed independently.

.. table:: **Table 1** URI parameter description

   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                                                                                                                                                                                                                                                                 |
   +===================================+=============================================================================================================================================================================================================================================================================================================================================================================================================================+
   | URI-scheme                        | Protocol used to transmit requests. HTTPS must be used in MRS APIs.                                                                                                                                                                                                                                                                                                                                                         |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MRS Manager floating IP address   | IP address for logging in to MRS Manager.                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | For clusters that support Kerberos authentication (security clusters), the floating IP address (cluster console address) of the cluster is displayed on the basic cluster information page.                                                                                                                                                                                                                                 |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | For a non-security cluster that does not support Kerberos authentication, you can log in to the Master2 node of the cluster `using VNC <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0083.html>`__ and run the **ifconfig** command to view the floating IP address of the cluster. **eth0:wsom** indicates the floating IP address of MRS Manager. The value of the **inet** parameter is the floating IP address. |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |                                   |                                                                                                                                                                                                                                                                                                                                                                                                                             |
   |                                   |    If the floating IP address of MRS Manager cannot be queried on the Master2 node, switch to the Master1 node to query and record the floating IP address.                                                                                                                                                                                                                                                                 |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | MRS Manager port                  | Port number for logging in to the MRS Manager. The default value is **28443**.                                                                                                                                                                                                                                                                                                                                              |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | resource-path                     | The path for accessing an API. Obtain the value from the URI of the API, for example, **v3/auth/tokens**.                                                                                                                                                                                                                                                                                                                   |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Query string                      | Optional. For example, API version or resource selection criterion.                                                                                                                                                                                                                                                                                                                                                         |
   +-----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Request Mode
------------

HTTP-based request methods, which are also called operations or actions, specify the type of operations that you are requesting.

.. table:: **Table 2** HTTP method

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

Request Header
--------------

A request header consists of several header fields. Each header field consists of a field name, a colon (:), and a field value.

Optional additional request header field, such as the field required by a specified URI and HTTP method. :ref:`Table 3 <mrs_02_1019__en-us_topic_0125376273_tb3f5c5f3dfb84fce8aa08057e60545ac>` lists common MRS request headers. For details about the request authentication information, see :ref:`Authentication <mrs_02_0009>`.

.. _mrs_02_1019__en-us_topic_0125376273_tb3f5c5f3dfb84fce8aa08057e60545ac:

.. table:: **Table 3** Common request header fields

   +-----------------+-------------------------------------------------------------+---------------------------------------------------------------------------------------------+------------------+
   | Name            | Description                                                 | Mandatory                                                                                   | Example          |
   +=================+=============================================================+=============================================================================================+==================+
   | Content-type    | Specifies the request body MIME type.                       | Yes                                                                                         | application/json |
   +-----------------+-------------------------------------------------------------+---------------------------------------------------------------------------------------------+------------------+
   | Content-Length  | Specifies the length of the request body. The unit is byte. | This field is mandatory for POST and PUT requests, but must be left blank for GET requests. | 3495             |
   +-----------------+-------------------------------------------------------------+---------------------------------------------------------------------------------------------+------------------+
   | X-Language      | Request language. The options are as follows:               | No                                                                                          | en-us            |
   |                 |                                                             |                                                                                             |                  |
   |                 | **en-us**: English                                          |                                                                                             |                  |
   +-----------------+-------------------------------------------------------------+---------------------------------------------------------------------------------------------+------------------+

.. note::

   For details about other headers, see the HTTP protocol.

Request Body
------------

A request body is generally sent in a structured format (for example, JSON or XML). It corresponds to **Content-type** in the request header and is used to transfer content other than the request header.

Response Header
---------------

A response header contains the following parts:

-  HTTP status code, which consists of three digits (2\ *xx* to 5\ *xx*). 2\ *xx* indicates a success response. 4\ *xx* or 5\ *xx* indicates a failure response; Alternatively, a service-defined status code may be returned, as described in this document.

-  Optional additional header fields to support the request's response, such as **Content-type**. For details about common message headers, see :ref:`Table 4 <mrs_02_1019__en-us_topic_0125376273_ta1929fc30fc14e1ebf1cf848648c76d8>`.

   .. _mrs_02_1019__en-us_topic_0125376273_ta1929fc30fc14e1ebf1cf848648c76d8:

   .. table:: **Table 4** Common response headers

      +----------------+----------------------------------------------------------------------------------------------+-----------+-------------------------------+
      | Parameter      | Description                                                                                  | Mandatory | Examples                      |
      +================+==============================================================================================+===========+===============================+
      | Date           | (Standard HTTP header). The time when a response is sent, whose format follows RFC 822.      | Yes       | Mon, 12 Nov 2007 15:55:01 GMT |
      +----------------+----------------------------------------------------------------------------------------------+-----------+-------------------------------+
      | Server         | (Standard HTTP header). The software information that the server uses to process the request | Yes       | Apache                        |
      +----------------+----------------------------------------------------------------------------------------------+-----------+-------------------------------+
      | Content-Length | (Standard HTTP header). The size of a message body in decimal number of bytes                | No        | xxx                           |
      +----------------+----------------------------------------------------------------------------------------------+-----------+-------------------------------+
      | Content-type   | (Standard HTTP header) Media type of the message body sent to a receiver                     | Yes       | application/json              |
      +----------------+----------------------------------------------------------------------------------------------+-----------+-------------------------------+

Response Body
-------------

A response body is generally returned in a structured format (for example, JSON or XML). It corresponds to **Content-type** in the response header and is used to transfer content other than the response header.

Initiating a Request
--------------------

You can initiate a request based on the constructed request message using any of the following:

-  cURL

   cURL is a command-line tool used to perform URL operations and transmit information. It serves as an HTTP client that can send HTTP requests to the server and receive response messages. cURL is applicable to API debugging. For more information about cURL, visit https://curl.haxx.se/.

-  Encoding

   You can call APIs using code to assemble, send, and process request messages.

-  REST client

   Both Mozilla Firefox and Google Chrome provide a graphical browser plug-in, that is, REST client, to send and process requests. For Mozilla Firefox, see `Firefox REST Client <https://addons.mozilla.org/en-US/firefox/addon/rest-client-apishub/>`__. For Google Chrome, see `Chrome REST Client <https://code.google.com/archive/p/rest-client>`__.
