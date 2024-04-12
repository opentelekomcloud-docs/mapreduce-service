:original_name: mrs_01_24795.html

.. _mrs_01_24795:

Error Is Reported When the Job of Capturing Data From PgSQL to Hudi Is Started
==============================================================================

Symptom
-------

The error message "Record key is empty" is displayed when the job of capturing data from PgSQL to Hudi is started.

|image1|

Possible Causes
---------------

The primary key parameter **table.primarykey.mapping** of the Hudi table is not configured.

Procedure
---------

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **CDL**. Click the hyperlink next to **CDLService UI** to access the CDLService web UI. On the data synchronization job list page, locate the row that contains the target job and choose **More** > **Stop**. After the job is stopped, choose **More** > **Edit**.
#. Configure the **table.primarykey.mapping** parameter on the Hudi table attribute configuration page and click **Save**. For details about the parameter, see :ref:`Table 6 <mrs_01_24239__table12483144010172>`.
#. On the data synchronization job list page, locate the row containing the target job and click **Start** to restart the job.

.. |image1| image:: /_static/images/en-us_image_0000001532632208.png
