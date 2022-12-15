:original_name: mrs_01_0141.html

.. _mrs_01_0141:

Hive on Hue
===========

Hue provides the Hive GUI management function so that users can query Hive data in GUI mode.

How to Use Query Editor
-----------------------

Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

In the navigation tree on the left, click |image1| and choose **Hive**. The **Hive** page is displayed.

-  Running Hive HQL statements

   Select the target database on the left. You can also click |image2| in the upper right corner and enter the target database name to search for the target database.

   Enter a Hive HQL statement in the text box and click |image3| or press **Ctrl+Enter** to run the HQL statement. The execution result is displayed on the **Result** tab page.

-  Analyzing Hive HQL statements

   Select the target database on the left, enter the Hive HQL statement in the text box, and click |image4| to compile the HQL statement and check whether the statement is correct. The execution result is displayed under the text editing box.

-  Saving HQL statements

   Enter the Hive HQL statement in the text box, click |image5| in the upper right corner, and enter the name and description. You can view the saved statements on the **Saved Queries** tab page.

-  Viewing historical records

   Click **Query History** to view the HQL running status. You can view the history of all the statements or only the saved statements. If many historical records exist, you can enter keywords in the text box to search for desired records.

-  Configuring advanced query

   Click |image6| in the upper right corner to configure the file, function, and settings.

-  Viewing the information of shortcut keys

   Click |image7| in the upper right corner to view information about all shortcut keys.

How to Use Metadata Browser
---------------------------

Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

-  Viewing metadata of Hive tables

   Click |image8| in the navigation tree on the left and click a table name. The metadata of the Hive table is displayed.

-  Managing metadata of Hive tables

   On the metadata information page of a Hive table:

   -  Click **Import** in the upper right corner to import data.

   -  Click **Overview** to view the location of the table file in the **PROPERTIES** field.

      View the field information of each column in a Hive table and manually add description information. Note that the added description information is not the field comments in the Hive table.

   -  Click **Sample** to browse data.

-  Managing Hive metadata tables

   Click |image9| in the left list to create a table based on the uploaded file in the database. You can also manually create a table.

.. caution::

   The Hue page is used to view and analyze data such as files and tables. Do not perform high-risk management operations such as deleting objects on the page. If an operation is required, you are advised to perform the operation on each component after confirming that the operation has no impact on services. For example, you can use the HDFS client to perform operations on HDFS files and use the Hive client to perform operations on Hive tables.

Typical Scenarios
-----------------

On the Hue page, create a Hive table as follows:

#. Click |image10| at the upper left corner of Hue web UI and select the Hive instance to be operated to enter the Hive command execution page.

#. Enter an HQL statement in the command input box, for example:

   **create table hue_table(id int,name string,company string) row format delimited fields terminated by ',' stored as textfile;**

   Click |image11| to execute the HQL statements.

#. Enter the following command in the command input box:

   **show tables;**

   Click |image12| to view the created table **hue_table** in **Result**.

.. |image1| image:: /_static/images/en-us_image_0000001296250192.png
.. |image2| image:: /_static/images/en-us_image_0000001349090389.png
.. |image3| image:: /_static/images/en-us_image_0000001296090544.png
.. |image4| image:: /_static/images/en-us_image_0000001349090393.png
.. |image5| image:: /_static/images/en-us_image_0000001349090385.png
.. |image6| image:: /_static/images/en-us_image_0000001348770577.png
.. |image7| image:: /_static/images/en-us_image_0000001295930720.png
.. |image8| image:: /_static/images/en-us_image_0000001295930724.png
.. |image9| image:: /_static/images/en-us_image_0000001295770764.png
.. |image10| image:: /_static/images/en-us_image_0000001296090548.png
.. |image11| image:: /_static/images/en-us_image_0000001349170289.png
.. |image12| image:: /_static/images/en-us_image_0000001296250196.png
