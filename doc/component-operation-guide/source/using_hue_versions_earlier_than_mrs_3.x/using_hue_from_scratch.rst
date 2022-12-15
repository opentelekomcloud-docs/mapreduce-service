:original_name: mrs_01_1020.html

.. _mrs_01_1020:

Using Hue from Scratch
======================

Hue provides the file browser function using a graphical user interface (GUI) so that you can view files and directories on Hive.

Prerequisites
-------------

You have installed Hive and Hue, and the Kerberos authentication cluster in the running state.

Procedure
---------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0370>`.

#. Open the Hue web UI and choose **Query Editors** > **Hive**.

#. In **Databases**, select a Hive database, the default database is **default**.

   The system displays all available tables. You can enter a keyword of the table name to search for the desired table.

#. Click the desired table name. All columns in the table are displayed.

#. .. _mrs_01_1020__li62672328145244:

   Enter the HiveQL statements in the area for editing.

   **create table hue_table(id int,name string,company string) row format delimited fields terminated by ',' stored as textfile;**

   Click |image1| and select **Explain**. The editor checks the syntax and execution plan of the entered HiveQL statements. If the statements have syntax errors, the editor reports **Error while compiling statement**.

#. Click |image2|, and select the engine for executing the HiveQL statements.

#. Click |image3| to execute the HiveQL statements.

#. In the command text box, enter **show tables;** and click |image4|. Check whether the **hue-table** table created in :ref:`5 <mrs_01_1020__li62672328145244>` exists in the result.

.. |image1| image:: /_static/images/en-us_image_0000001349090137.jpg
.. |image2| image:: /_static/images/en-us_image_0000001296249940.png
.. |image3| image:: /_static/images/en-us_image_0000001296090292.jpg
.. |image4| image:: /_static/images/en-us_image_0000001295770504.png
