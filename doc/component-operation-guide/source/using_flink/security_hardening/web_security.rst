:original_name: mrs_01_1585.html

.. _mrs_01_1585:

Web Security
============

Coding Specifications
---------------------

Note: The same coding mode is used on the web service client and server to prevent garbled characters and to enable input verification.

Security hardening: apply UTF-8 to response messages of web server.

Whitelist-based Filter of IP Addresses
--------------------------------------

Note: IP filter must be added to the web server to filter unauthorized requests from the source IP address and prevent unauthorized login.

Security: Add **jobmanager.web.allow-access-address** to enable the IP filter. By default, only Yarn users are supported.

.. note::

   After the client is installed, you need to add the IP address of the client node to the **jobmanager.web.allow-access-address** configuration item.

Preventing Sending the Absolute Paths to the Client
---------------------------------------------------

Note: If an absolute path is sent to a client, the directory structure of the server is exposed, increasing the risk that attackers know and attack the system.

Security hardening: If the Flink configuration file contains a parameter starting with a slash (/), the first-level directory is deleted.

Same-origin Policy
------------------

The same-source policy applies to MRS 3.x or later.

If two URL protocols have same hosts and ports, they are of the same origin. Protocols of different origins cannot access each other, unless the source of the visitor is specified on the host of the service to be visited.

Security hardening: The default value of the header of the response header **Access-Control-Allow-Origin** is the IP address of ResourceManager on Yarn clusters. If the IP address is not from Yarn, mutual access is not allowed.

Preventing Sensitive Information Disclosure
-------------------------------------------

Sensitive information disclosure prevention is applicable to MRS 3.x or later.

Web pages containing sensitive data must not be cached, to avoid leakage of sensitive information or data crosstalk among users who visit the internet through the proxy server.

Security hardening: Add **Cache-control**, **Pragma**, **Expires** security header. The default value is **Cache-Control: no-store**, **Pragma: no-cache**, and **Expires: 0**.

The security hardening stops contents interacted between Flink and web server from being cached.

Anti-Hijacking
--------------

Anti-hijacking applies to MRS 3.x or later.

Since hotlinking and clickjacking use framing technologies, security hardening is required to prevent attacks.

Security hardening: Add **X-Frame-Options** security header to specify whether the browser will load the pages from **iframe**, **frame** or **object**. The default value is **X-Frame-Options: DENY**, indicating that no pages can be nested to **iframe**, **frame** or **object**.

Logging calls of the Web Service APIs
-------------------------------------

This function applies to MRS 3.x or later.

Calls of the **Flink webmonitor restful** APIs are logged.

The **jobmanager.web.accesslog.enable** can be added in the **access log**. The default value is **true**. Logs are stored in a separate **webaccess.log** file.

Cross-Site Request Forgery Prevention
-------------------------------------

Cross-site request forgery (CSRF) prevention applies to MRS 3.x or later.

In **Browser/Server** applications, CSRF must be prevented for operations involving server data modification, such as adding, modifying, and deleting. The CSRF forces end users to execute non-intended operations on the current web application.

Security hardening: Only two post APIs, one delete API, and get interfaces are reserve for modification requests. All other APIs are deleted.

Troubleshooting
---------------

This function applies to MRS 3.x or later.

When the application is abnormal, exception information is filtered, logged, and returned to the client.

Security hardening

-  A default error message page to filter information and log detailed error information.
-  Four configuration parameters are added to ensure that the error page is switched to a specified URL provided by FusionInsight, preventing exposure of unnecessary information.

   .. table:: **Table 1** Parameter description

      +---------------------------------+--------------------------------------------------------------------------------------+---------------+-----------+
      | Parameter                       | Description                                                                          | Default Value | Mandatory |
      +=================================+======================================================================================+===============+===========+
      | jobmanager.web.403-redirect-url | Web page access error 403. If 403 error occurs, the page switch to a specified page. | ``-``         | Yes       |
      +---------------------------------+--------------------------------------------------------------------------------------+---------------+-----------+
      | jobmanager.web.404-redirect-url | Web page access error 404. If 404 error occurs, the page switch to a specified page. | ``-``         | Yes       |
      +---------------------------------+--------------------------------------------------------------------------------------+---------------+-----------+
      | jobmanager.web.415-redirect-url | Web page access error 415. If 415 error occurs, the page switch to a specified page. | ``-``         | Yes       |
      +---------------------------------+--------------------------------------------------------------------------------------+---------------+-----------+
      | jobmanager.web.500-redirect-url | Web page access error 500. If 500 error occurs, the page switch to a specified page. | ``-``         | Yes       |
      +---------------------------------+--------------------------------------------------------------------------------------+---------------+-----------+

HTML5 Security
--------------

HTML5 security applies to MRS 3.x or later.

HTML5 is a next generation web development specification that provides new functions and extend the labels for developers. These new labels and functions increase the attack surface and pose attack risks (such as cross-domain resource sharing, client storage, WebWorker, WebRTC, and WebSocket).

Security hardening: Add the **Access-Control-Allow-Origin** parameter. For example, if you want to enable the cross-domain resource sharing, configure the **Access-Control-Allow-Origin** parameter of the HTTP response header.

.. note::

   Flink does not involve security risks of functions such as storage on the client, WebWorker, WebRTC, and WebSocket.
