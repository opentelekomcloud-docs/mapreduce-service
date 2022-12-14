:original_name: mrs_01_24464.html

.. _mrs_01_24464:

What Should I Do If Data Failed to Be Synchronized to a Hive Parquet Table Using HCatalog?
==========================================================================================

Question
--------

When the partition fields in a Hive parquet table are not of the string type, data in the table can be synchronized only using HCatalog. What should I do if the following error message is displayed during data synchronization?

|image1|

Answer
------

#. Delete the restricted code in the **SqoopHCatUtilities** class of Sqoop.
#. Change the value of the **hive.metastore.integral.jdo.pushdown** parameter in the **hive-site.xml** file on the Hive client to **true**.

.. |image1| image:: /_static/images/en-us_image_0000001441210777.png
