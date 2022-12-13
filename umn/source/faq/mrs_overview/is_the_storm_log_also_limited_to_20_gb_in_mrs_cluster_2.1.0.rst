:original_name: en-us_topic_0000001145676237.html

.. _en-us_topic_0000001145676237:

Is the Storm Log also limited to 20 GB in MRS cluster 2.1.0?
============================================================

In MRS cluster 2.1.0, the Storm log cannot exceed 20 GB. If the Storm log exceeds 20 GB, the log files will be deleted cyclically. Logs are stored on the system disk, therefore, the log space is limited. If you want to keep the log for longer time, mount the log directory to storage media.
