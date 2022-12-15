:original_name: mrs_01_0131.html

.. _mrs_01_0131:

Using Hue from Scratch
======================

Hue aggregates interfaces which interact with most Apache Hadoop components and enables you to use Hadoop components with ease on a web UI. You can operate components such as HDFS, Hive, HBase, Yarn, MapReduce, Oozie, and Spark SQL on the Hue web UI.

Prerequisites
-------------

You have installed Hue, and the Kerberos authentication cluster is in the running state.

Procedure
---------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

#. In the navigation tree on the left, click the editor icon |image1| and choose **Hive**.

#. Select a Hive database from the **Database** drop-down list box. The default database is **default**.

   The system displays all available tables. You can enter a keyword of the table name to search for the desired table.

#. Click the desired table name. All columns in the table are displayed.

#. .. _mrs_01_0131__li62672328145244:

   Enter the HiveQL statements in the area for editing.

   **create table hue_table(id int,name string,company string) row format delimited fields terminated by ',' stored as textfile;**

#. Click |image2| to execute the HiveQL statements.

#. In the command text box, enter **show tables;** and click |image3|. Check whether the **hue_table** table created in :ref:`5 <mrs_01_0131__li62672328145244>` exists in the **Result**.

.. |image1| image:: /_static/images/en-us_image_0000001348770605.png
.. |image2| image:: /_static/images/en-us_image_0000001349289901.jpg
.. |image3| image:: /_static/images/en-us_image_0000001296250224.png
