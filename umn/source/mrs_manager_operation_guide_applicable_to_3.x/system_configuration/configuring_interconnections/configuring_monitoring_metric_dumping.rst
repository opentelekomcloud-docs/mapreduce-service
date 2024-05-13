:original_name: admin_guide_000156.html

.. _admin_guide_000156:

Configuring Monitoring Metric Dumping
=====================================

Scenario
--------

The monitoring data reporting function writes the monitoring data collected in the system into a text file and uploads the file to a specified server in FTP or SFTP mode.

Before using this function, you need to perform related configurations on MRS Manager.

Procedure
---------

#. Log in to MRS Manager.

#. Choose **System** > **Interconnection** > **Upload Performance Data**.

#. Toggle on **Upload Performance Data**.

   The performance data upload service is disabled by default. |image1| indicates that the service is enabled.

#. Set the upload parameters according to :ref:`Table 1 <admin_guide_000156__table36700465>`.

   .. _admin_guide_000156__table36700465:

   .. table:: **Table 1** Upload parameters

      +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter               | Description                                                                                                                                                                                                                   |
      +=========================+===============================================================================================================================================================================================================================+
      | FTP IP Address Mode     | Specifies the server IP address mode. This parameter is mandatory. The value can be **IPV4** or **IPV6**.                                                                                                                     |
      +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | FTP IP Address          | Specifies the IP address of the FTP server for storing monitoring files after the monitoring metric data is interconnected. This parameter is mandatory.                                                                      |
      +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | FTP Port                | Specifies the port for connecting to the FTP server. This parameter is mandatory.                                                                                                                                             |
      +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | FTP Username            | Specifies the username for logging in to the FTP server. This parameter is mandatory.                                                                                                                                         |
      +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | FTP Password            | Specifies the password for logging in to the FTP server. This parameter is mandatory.                                                                                                                                         |
      +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Save Path               | Specifies the path for storing monitoring files on the FTP server. This parameter is mandatory.                                                                                                                               |
      +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Dump Interval (second)  | Specifies the interval at which monitoring files are periodically stored on the FTP server, in seconds. This parameter is mandatory.                                                                                          |
      +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Dump Mode               | Specifies the protocol used for sending monitoring files. This parameter is mandatory. The value can be **SFTP** or **FTP**. You are advised to use the SFTP mode based on SSH v2. Otherwise, security risks may be incurred. |
      +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | SFTP Service Public Key | Specifies the public key of the FTP server. This parameter is optional. It is valid only when **Dump Mode** is set to **SFTP**.                                                                                               |
      +-------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK**.

   .. note::

      If the dump mode is SFTP and the public key of the SFTP service is empty, the system displays a security risk warning. You need to evaluate the security risk and then save the configuration.

Data Format
-----------

After the configuration is complete, the monitoring data reporting function periodically writes monitoring data in the cluster to text files and reports the files to the corresponding FTP/SFTP service based on the configured reporting period.

-  Principles for generating monitoring files

   -  The monitoring metrics are written to files generated every 30, 60, and 300 seconds based on the metric collection period.

      30s: real-time metrics that are collected every 30s by default

      60s: real-time metrics that are collected every 60s by default

      300s: all metrics that are not collected every 30s or 60s

   -  File name format: *metric_{Interval}_{File creation time YYYYMMDDHHMMSS}.log*

      Example: **metric_60_20160908085915.log**

      **metric_300_20160908085613.log**

-  Monitoring file content

   -  Format of monitoring files:

      "Cluster ID|Cluster name|Displayed name|Service name|Metric ID|Collection time|Collection host@m@Sub-metric|Unit|Metric value", where fields are separated using vertical bars (|). For example:

      .. code-block::

         1|xx1|Host|Host|10000413|2019/06/18 10:05:00|189-66-254-146|KB/s|309.910
         1|xx1|Host|Host|10000413|2019/06/18 10:05:00|189-66-254-152|KB/s|72.870
         2|xx2|Host|Host|10000413|2019/06/18 10:05:00|189-66-254-163|KB/s|100.650

      Note: The actual files are not in that format.

   -  Interval for uploading monitoring files:

      The interval for uploading monitoring files can be set using the **Dump Interval (second)** parameter on the page. Currently, the interval can range from **30** to **300**. After the configuration is complete, the system periodically uploads files to the corresponding FTP/SFTP server at the specified interval.

-  Monitoring metric description file

   -  Metric set file

      The metric set file **all-shown-metric-zh_CN** contains detailed information about all metrics. After obtaining the metric IDs from the files reported by the third-party system, you can query details about the metrics from the metric set file.

      Location of the metric set file:

      Active and standby OMS nodes: {*MRS installation path*} **/om-server/om/etc/om/all-shown-metric-zh_CN**

      Content of the metric set file:

      .. code-block::

         Real-Time Metric ID,5-Minute Metric ID,Metric Name,Metric Collection Period (s),Collected by Default,Service Belonged To,Role Belonged To
         00101,10000101,JobHistoryServer non-heap memory usage,30,false,Mapreduce,JobHistoryServer
         00102,10000102,JobHistoryServer non-heap memory allocation volume,30,false,Mapreduce,JobHistoryServer
         00103,10000103,JobHistoryServer heap memory usage,30,false,Mapreduce,JobHistoryServer
         00104,10000104,JobHistoryServer heap memory allocation volume,30,false,Mapreduce,JobHistoryServer
         00105,10000105,Number of blocked threads,30,false,Mapreduce,JobHistoryServer
         00106,10000106,Number of running threads,30,false,Mapreduce,JobHistoryServer
         00107,10000107,GC time,30,false,Mapreduce,JobHistoryServer
         00110,10000110,JobHistoryServer CPU usage,30,false,Mapreduce,JobHistoryServer
         ...

   -  Field description of critical metrics

      **Real-Time Metric ID**: indicates the ID of the metric whose collection period is 30s or 60s.

      **5-Minute Metric ID**: indicates the ID of a 5-minute (300s) metric.

      **Metric Collection Period (s)**: indicates the collection period of real-time metrics. The value can be **30** or **60**.

      **Service Belonged To**: indicates the name of the service to which a metric belongs, for example, HDFS and HBase.

      **Role Belonged To**: indicates the name of the role to which a metric belongs, for example, JobServer and RegionServer.

   -  Description

      For metrics whose collection period is 30s/60s, you can find the corresponding metric description by referring to the first column, that is, **Real-Time Metric ID**.

      For metrics whose collection period is 300s, you can find the corresponding metric description by referring to the second column, that is, **5-Minute Metric ID**.

.. |image1| image:: /_static/images/en-us_image_0000001392414386.png
