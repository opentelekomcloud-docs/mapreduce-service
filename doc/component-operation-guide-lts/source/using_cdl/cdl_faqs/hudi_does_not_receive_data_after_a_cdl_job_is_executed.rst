:original_name: mrs_01_24793.html

.. _mrs_01_24793:

Hudi Does Not Receive Data After a CDL Job Is Executed
======================================================

Symptom
-------

After the CDL job for capturing data to Hudi is executed, related data exists in Kafka, but no record exists in Spark RDD, no related data exists in Hudi, and the error message "TopicAuthorizationException: No authorized to access topics" is displayed.

Possible Causes
---------------

The current user does not have the permission to consume Kafka data.

Procedure
---------

#. Log in to FusionInsight Manager and choose **System** > **Permission** > **User**. Locate the row containing the user who submitted the CDL job, click **Modify**, add the **kafkaadmin** user group, and click **OK**.
#. On FusionInsight Manager, choose **Cluster** > **Services** > **CDL**. Click the hyperlink next to **CDLService UI** to access the CDLService web UI and restart the job.
