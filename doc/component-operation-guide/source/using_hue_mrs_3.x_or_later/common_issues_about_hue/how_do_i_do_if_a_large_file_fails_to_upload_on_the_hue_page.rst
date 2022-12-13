:original_name: mrs_01_2367.html

.. _mrs_01_2367:

How Do I Do If a Large File Fails to Upload on the Hue Page?
============================================================

Question
--------

What can I do when a large file fails to be uploaded on the Hue page?

Answer
------

#. You are advised to run commands on the client to upload large files instead of using the Hue file browser.
#. If you must use Hue to upload the file, perform the following steps to modify Httpd parameters:

   a. Log in to the active management node as user **omm**.

   b. Run the following command to edit the **httpd.conf** file:

      **vi $BIGDATA_HOME/om-server/Apache-httpd-*/conf/httpd.conf**

   c. Search for **21201** and add **RequestReadTimeout handshake=0 header=0 body=0** to the **</VirtualHost>** configuration, as shown in the following:

      .. code-block::

         ...
         <VirtualHost *:21201>
             ServerName https://10.112.16.93:21201
             AllowEncodedSlashes On
             SSLProxyEngine On
             ProxyRequests Off
             TraceEnable off
             ProxyTimeout  1200
             RewriteEngine on
             RewriteMap proxylist dbm:${BIGDATA_ROOT_HOME}/om-server_*/Apache-httpd-*/conf/proxylist.dbm

             RewriteRule ^(\/.*)$  ${proxylist:/Hue/Hue/21201}$1 [E=TARGET_PATH:$1,L,P]

             Header edit Location ^(?!https://10.112.16.93:20009|https://10.112.16.93:21201)http[s]?://[^/]*(.*)$  https://10.112.16.93:21201$1

             ProxyPassReverseCookiePath / / interpolate

             SSLEngine On
             SSLProxyProtocol  All +TLSv1.2 -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
             SSLProtocol ALL +TLSv1.2 -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
             SSLCipherSuite ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:DHE-DSS-AES256-GCM-SHA384:DHE-RSA-AES256-GCM-SHA384:DHE-DSS-AES128-GCM-SHA256:DHE-RSA-AES128-GCM-SHA256
             SSLProxyCheckPeerName off
             SSLProxyCheckPeerCN off
             SSLCertificateFile "${BIGDATA_ROOT_HOME}/om-server_*/Apache-httpd-*/conf/security/proxy_ssl.cert"
             SSLCertificateKeyFile "${BIGDATA_ROOT_HOME}/om-server_*/Apache-httpd-*/conf/security/server.key"
             SSLProxyCACertificateFile ${BIGDATA_ROOT_HOME}/om-server_*/apache-tomcat-*/conf/security/tomcat.crt
             SSLCertificateChainFile "${BIGDATA_ROOT_HOME}/om-server_*/Apache-httpd-2.4.39/conf/security/proxy_chain.cert"
             RequestReadTimeout handshake=0 header=0 body=0
         </VirtualHost>
         ...

   d. Run the **pkill -9 httpd** command to stop the httpd process and wait for it to automatically restart.
