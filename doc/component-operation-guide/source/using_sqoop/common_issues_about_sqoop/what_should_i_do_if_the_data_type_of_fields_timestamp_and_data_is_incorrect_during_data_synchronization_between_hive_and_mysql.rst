:original_name: mrs_01_24465.html

.. _mrs_01_24465:

What Should I Do If the Data Type of Fields timestamp and data Is Incorrect During Data Synchronization Between Hive and MySQL?
===============================================================================================================================

Question
--------

What should I do if the data type of fields timestamp and data is incorrect during data synchronization between Hive and MySQL?

|image1|

Answer
------

-  Forcibly convert the data type of the timestamp field in the Sqoop source package to be the same as that in Hive.
-  Change the data type of the timestamp field in Hive to String.

.. |image1| image:: /_static/images/en-us_image_0000001296249912.png
