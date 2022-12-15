:original_name: admin_guide_000086.html

.. _admin_guide_000086:

Configuring Audit Log Dumping
=============================

Scenario
--------

The audit logs of FusionInsight Manager are stored in the database by default. If the audit logs are retained for a long time, the disk space of the data directory may be insufficient. To store audit logs to another archive server, administrators can set the required dump parameters to automatically dump these logs. This facilitates the management of audit logs.

If you do not configure the audit log dumping, the system automatically saves the audit logs to a file when the number of audit logs reaches 100,000 pieces. The save path is **${BIGDATA_DATA_HOME} /dbdata_om/dumpData/iam/operatelog** on the active management node. The file name format is **OperateLog_store\_**\ *YY_MM_DD_HH_MM_SS*\ **.csv**. The maximum number of historical audit log files is 50.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **Audit** > **Configuration**.

#. Click the switch on the right of **Audit Log Dumping Flag**.

   **Audit Log Dump** is disabled by default. If |image1| is displayed, **Audit Log Dump** is enabled.

#. Set the dump parameters based on information provided in :ref:`Table 1 <admin_guide_000086__table61365090>`

   .. _admin_guide_000086__table61365090:

   .. table:: **Table 1** Audit log dump parameters

      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
      | Parameter             | Description                                                                                                                                                                                                                                                | Value                                       |
      +=======================+============================================================================================================================================================================================================================================================+=============================================+
      | SFTP IP Mode          | Mode of the destination IP address. The value can be **IPv4** or **IPv6**.                                                                                                                                                                                 | IPv4                                        |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
      | SFTP IP               | SFTP server for storing dumped audit logs. You are advised to use the SFTP service based on SSH v2 to prevent security risks.                                                                                                                              | **192.168.10.51** (example value)           |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
      | SFTP Port             | Connection port of the SFTP server for storing dumped audit logs                                                                                                                                                                                           | **22** (example value)                      |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
      | Save Path             | Path for storing audit logs on the SFTP server                                                                                                                                                                                                             | **/opt/omm/oms/auditLog** (example value)   |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
      | SFTP Username         | User name for logging in to the SFTP server                                                                                                                                                                                                                | **root** (example value)                    |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
      | SFTP Password         | Password for logging in to the SFTP server                                                                                                                                                                                                                 | *Password for logging into the SFTP server* |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
      | SFTP Public key       | Specifies the public key of the SFTP server. This parameter is optional. You are advised to set the public key of the SFTP server. Otherwise, security risks may exist.                                                                                    | ``-``                                       |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
      | Dumping Mode          | Dump mode. Value options are as follows:                                                                                                                                                                                                                   | -  By Quantity                              |
      |                       |                                                                                                                                                                                                                                                            | -  By Time                                  |
      |                       | -  **By Quantity**: If the number of pieces of logs reaches the value of this parameter (**100000** by default), the logs are dumped.                                                                                                                      |                                             |
      |                       | -  **By Time**: specifies the date when logs are dumped. The dumping frequency is once a year.                                                                                                                                                             |                                             |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+
      | Dumping Date          | This parameter is available only when **Dumping Mode** is set to **By time**. After you select a dump date, the system starts dumping on this date. The logs to be dumped include all the audit logs generated before January 1 00:00 of the current year. | 11-06                                       |
      +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------+

   .. note::

      If the SFTP public key is empty, the system displays a security risk warning. Evaluate the security risk and then save the configuration.

#. Click **OK** to complete the settings.

   .. note::

      Key fields in the audit log dump file are as follows:

      -  **USERTYPE** indicates the user type. Value **0** indicates a human-machine user, and value **1** indicates a machine-machine user.
      -  **LOGLEVEL** indicates the security level. Value **0** indicates Critical, value **1** indicates Major, value **2** indicates Minor, and value **3** indicates Warning.
      -  **OPERATERESULT** indicates the operation result. Value **0** indicates that the operation is successful, and value **1** indicates that the operation is failed.

.. |image1| image:: /_static/images/en-us_image_0263899218.png
