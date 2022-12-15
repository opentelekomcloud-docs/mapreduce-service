:original_name: mrs_01_0235.html

.. _mrs_01_0235:

Configuring Monitoring Metric Dumping
=====================================

You can configure interconnection parameters on MRS Manager to save monitoring metric data to a specified FTP server using the FTP or SFTP protocol. In this way, MRS clusters can interconnect with third-party systems. The FTP protocol does not encrypt data, which brings potential security risks. Therefore, the SFTP protocol is recommended.

MRS Manager supports the collection of all the monitoring metric data in the managed clusters. The collection period is 30 seconds, 60 seconds, or 300 seconds. The monitoring metric data is stored to different monitoring files on the FTP server by collection period. The monitoring file naming rule is in the "*Cluster name*\ \_\ **metric**\ \_\ *Monitoring metric data collection period*\ \_\ *File saving time*\ **.log**" format.

Prerequisites
-------------

The ECS corresponding to the dump server must be in the same VPC as the Master node of the MRS cluster, and the Master node can access the IP address and specified port of the dump server. The FTP service on the dump server is running properly.

Procedure
---------

#. On MRS Manager, click **System**.

#. In **Configuration**, click **Configure Monitoring Metric Dump** under **Monitoring and Alarm**.

#. :ref:`Table 1 <mrs_01_0235__en-us_topic_0035209602_table50198556114935>` describes dump parameters.

   .. _mrs_01_0235__en-us_topic_0035209602_table50198556114935:

   .. table:: **Table 1** Dump parameters

      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter                         | Description                                                                                                                                                                                                  |
      +===================================+==============================================================================================================================================================================================================+
      | Dump Monitoring Metric            | Mandatory. This parameter specifies whether to enable the monitoring metric data interconnection function.spe                                                                                                |
      |                                   |                                                                                                                                                                                                              |
      |                                   | -  |image1|: Enabled.                                                                                                                                                                                        |
      |                                   | -  |image2|: Disabled.                                                                                                                                                                                       |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | FTP IP Address                    | Mandatory. This parameter specifies the FTP server for storing monitoring files after the monitoring indicator data is interconnected.                                                                       |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | FTP Port                          | Mandatory. This parameter specifies the port connected to the FTP server.                                                                                                                                    |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | FTP Username                      | Mandatory. This parameter specifies the username for logging in to the FTP server.                                                                                                                           |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | FTP Password                      | Mandatory. This parameter specifies the password for logging in to the FTP server.                                                                                                                           |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Save Path                         | Mandatory. This parameter specifies the path for storing monitoring files on the FTP server.                                                                                                                 |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Dump Interval (s)                 | Mandatory. This parameter specifies the interval at which monitoring files are periodically stored on the FTP server, in seconds.                                                                            |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Dump Mode                         | Mandatory. This parameter specifies the protocol used for sending monitoring files. This parameter is mandatory. The options are **FTP** and **SFTP**.                                                       |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | SFTP Public Key                   | Optional. This parameter specifies the public key of the FTP server and is valid only when **Dump Mode** is set to **SFTP**. You are advised to configure a public key. Otherwise, security risks may arise. |
      +-----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

#. Click **OK** to complete the settings.

.. |image1| image:: /_static/images/en-us_image_0000001349057789.png
.. |image2| image:: /_static/images/en-us_image_0000001349137681.png
