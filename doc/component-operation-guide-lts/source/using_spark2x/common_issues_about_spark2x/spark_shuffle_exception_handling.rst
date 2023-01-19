:original_name: mrs_01_24176.html

.. _mrs_01_24176:

Spark Shuffle Exception Handling
================================

Question
--------

In some scenarios, the following exception occurs in the Spark shuffle phase:

|image1|

Solution
--------

For JDBC:

Log in to FusionInsight Manager, change the value of the JDBCServer parameter **spark.authenticate.enableSaslEncryption** to **false**, and restart the corresponding instance.

For client jobs:

When the client submits the application, change the value of **spark.authenticate.enableSaslEncryption** in the **spark-defaults.conf** file to **false**.

.. |image1| image:: /_static/images/en-us_image_0000001348739993.png
