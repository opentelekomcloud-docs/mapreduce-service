:original_name: mrs_01_24794.html

.. _mrs_01_24794:

Error 104 or 143 Is Reported After a CDL Job Runs for a Period of Time
======================================================================

Symptom
-------

After an CDL job runs for a period of time, the YARN job fails and the status code **104** or **143** is returned.

Possible Causes
---------------

A large amount of data is captured to Hudi. As a result, the memory of the job is insufficient.

Procedure
---------

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **CDL**. Click the hyperlink next to **CDLService UI** to access the CDLService web UI. On the data synchronization job list page, locate the row that contains the target job and choose **More** > **Stop**. After the job is stopped, choose **More** > **Edit**.
#. Change the value of **max.rate.per.partition** of Hudi to **6000** and click **Save**.
#. On the data synchronization job list page, locate the row containing the target job and choose **More** > **Restart** to restart the job.
