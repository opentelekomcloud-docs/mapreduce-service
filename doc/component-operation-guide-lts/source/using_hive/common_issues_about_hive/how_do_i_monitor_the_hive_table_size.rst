:original_name: mrs_01_1758.html

.. _mrs_01_1758:

How Do I Monitor the Hive Table Size?
=====================================

Question
--------

How do I monitor the Hive table size?

Answer
------

The HDFS refined monitoring function allows you to monitor the size of a specified table directory.

Prerequisites
-------------

-  The Hive and HDFS components are running properly.
-  The HDFS refined monitoring function is normal.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **Cluster** > *Name of the desired cluster* > **Services** > **HDFS** > **Resource**.

#. Click the first icon in the upper left corner of **Resource Usage (by Directory)**, as shown in the following figure.

   |image1|

4. In the displayed sub page for configuring space monitoring, click **Add**.
5. In the displayed **Add a Monitoring Directory** dialog box, set **Name** to the name or the user-defined alias of the table to be monitored and **Path** to the path of the monitored table. Click **OK**. In the monitoring result, the horizontal coordinate indicates the time, and the vertical coordinate indicates the size of the monitored directory.

.. |image1| image:: /_static/images/en-us_image_0000001348739969.jpg
