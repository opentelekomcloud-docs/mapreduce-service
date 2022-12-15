:original_name: mrs_01_0270.html

.. _mrs_01_0270:

Configuring Audit Log Exporting Parameters
==========================================

Scenario
--------

If MRS audit logs are stored in the system for a long time, the disk space of the data directory may be insufficient. Therefore, you can set export parameters to automatically export audit logs to a specified directory on the OBS server timely, facilitating audit log management.

.. note::

   Audit logs exported to the OBS server include service audit logs and management audit logs.

   -  Service audit logs are automatically compressed and stored in the **/var/log/Bigdata/audit/bk/** directory on the active management node at 03:00 every day. The file name format is <*yyyy-MM-dd_HH-mm-ss*>\ **.tar.gz**. By default, a maximum of seven log files can be stored. If more than seven log files are stored, the system automatically deletes the log files generated seven days ago.
   -  The data range of management audit logs exported to OBS each time is from the last date when the logs are successfully exported to OBS to the date when the task is executed. When the number of management audit logs reaches 100,000, the system automatically dumps the first 90,000 audit logs to a local file and retains 10,000 audit logs in the database. The dumped log files are saved in the **${BIGDATA_DATA_HOME}/dbdata_om/dumpData/iam/operatelog** directory on the active management node. The file name format is **OperateLog_store**\ *\_YY_MM_DD_HH_MM_SS*\ **.csv**. A maximum of 50 historical audit log files can be saved.

Prerequisites
-------------

-  You have obtained the access key ID (AK) and secret access key (SK) of the account.
-  A parallel file system has been created in OBS.

Procedure
---------

#. On MRS Manager, click **System**.
#. Choose **Export Audit Log** under **Maintenance**.

   .. table:: **Table 1** Parameters for exporting audit logs

      +-----------------------+-------------------------------------------+----------------------------------------------------------------------------------------------------+
      | Parameter             | Value                                     | Description                                                                                        |
      +=======================+===========================================+====================================================================================================+
      | Export Audit Log      | -  |image1|                               | (Mandatory) Specifies whether to enable the audit log export function.                             |
      |                       | -  |image2|                               |                                                                                                    |
      |                       |                                           | -  |image3|: enables audit log exporting.                                                          |
      |                       |                                           |                                                                                                    |
      |                       |                                           | -  |image4|: disables audit log exporting.                                                         |
      +-----------------------+-------------------------------------------+----------------------------------------------------------------------------------------------------+
      | Start Time            | 7/24/2017 09:00:00 (example value)        | (Mandatory) Specifies the start time for exporting audit logs.                                     |
      +-----------------------+-------------------------------------------+----------------------------------------------------------------------------------------------------+
      | Period (days)         | 1 day (example value)                     | (Mandatory) Specifies the interval for exporting audit logs. The interval ranges from 1 to 5 days. |
      +-----------------------+-------------------------------------------+----------------------------------------------------------------------------------------------------+
      | Bucket                | mrs-bucket (example value)                | (Mandatory) Specifies the name of the OBS file system to which audit logs are exported.            |
      +-----------------------+-------------------------------------------+----------------------------------------------------------------------------------------------------+
      | OBS path              | **/opt/omm/oms/auditLog** (example value) | (Mandatory) Specifies the OBS path to which audit logs are exported.                               |
      +-----------------------+-------------------------------------------+----------------------------------------------------------------------------------------------------+
      | AK                    | *XXX* (example value)                     | (Mandatory) Specifies the user's access key ID.                                                    |
      +-----------------------+-------------------------------------------+----------------------------------------------------------------------------------------------------+
      | SK                    | *XXX* (example value)                     | (Mandatory) Specifies the user's secret access key.                                                |
      +-----------------------+-------------------------------------------+----------------------------------------------------------------------------------------------------+

   .. note::

      Audit logs are stored in **service_auditlog** and **manager_auditlog** on OBS, which are used to store service audit logs and management audit logs, respectively.

.. |image1| image:: /_static/images/en-us_image_0000001349257205.png
.. |image2| image:: /_static/images/en-us_image_0000001295738112.png
.. |image3| image:: /_static/images/en-us_image_0000001349137625.png
.. |image4| image:: /_static/images/en-us_image_0000001296217548.png
