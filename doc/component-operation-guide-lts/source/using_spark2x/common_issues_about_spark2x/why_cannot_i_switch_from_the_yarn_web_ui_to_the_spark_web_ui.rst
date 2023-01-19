:original_name: mrs_01_2056.html

.. _mrs_01_2056:

Why Cannot I Switch from the Yarn Web UI to the Spark Web UI?
=============================================================

Question
--------

In FusionInsight, the Spark application is run in yarn-client mode on the client. The following error occurs during the switch from the Yarn web UI to the application web UI:

|image1|

The YARN ResourceManager log shows the following information:

.. code-block::

   2016-07-21 16:35:27,099 | INFO  | Socket Reader #1 for port 8032 | Auth successful for mapred/hadoop.<System domain name>@<System domain name> (auth:KERBEROS) | Server.java:1388
   2016-07-21 16:35:27,105 | INFO  | 1526016381@qtp-1178290888-1015 | admin is accessing unchecked http://10.120.169.53:23011 which is the app master GUI of
   application_1468986660719_0045 owned by spark | WebAppProxyServlet.java:393
   2016-07-21 16:36:02,843 | INFO  | Socket Reader #1 for port 8032 | Auth successful for hive/hadoop.<System domain name>@<System domain name> (auth:KERBEROS) | Server.java:1388
   2016-07-21 16:36:02,851 | INFO  | Socket Reader #1 for port 8032 | Auth successful for hive/hadoop.<System domain name>@<System domain name> (auth:KERBEROS) | Server.java:1388
   2016-07-21 16:36:12,163 | WARN  | 1526016381@qtp-1178290888-1015 | /proxy/application_1468986660719_0045/: java.net.ConnectException: Connection timed out |
   Slf4jLog.java:76
   2016-07-21 16:37:03,918 | INFO  | Socket Reader #1 for port 8032 | Auth successful for hive/hadoop.<System domain name>@<System domain name> (auth:KERBEROS) | Server.java:1388
   2016-07-21 16:37:03,926 | INFO  | Socket Reader #1 for port 8032 | Auth successful for hive/hadoop.<System domain name>@<System domain name> (auth:KERBEROS) | Server.java:1388
   2016-07-21 16:37:11,956 | INFO  | AsyncDispatcher event handler | Updating application attempt appattempt_1468986660719_0045_000001 with final state: FINISHING,
   and exit status: -1000 | RMAppAttemptImpl.java:1253

Answer
------

On FusionInsight Manager, the IP address of the Yarn service is in the 192 network segment.

In Yarn logs, the IP address of Spark web UI read by Yarn is http://10.120.169.53:23011, which is in the 10 network segment. The IP addresses in the 192 network segment cannot communicate with those in the 10 network segment. As a result, the Spark web UI fails to be accessed.

Solution:

Log in to the client whose IP address is **10.120.169.53** and change the IP address in the **/etc/hosts** file to the IP address in the 192 network segment. Run the Spark application again. The Spark web UI is displayed.

.. |image1| image:: /_static/images/en-us_image_0000001349139601.png
