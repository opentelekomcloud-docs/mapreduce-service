:original_name: mrs_01_0135.html

.. _mrs_01_0135:

Using the Metadata Browser on the Hue Web UI
============================================

Scenario
--------

Users can use the Hue web UI to manage Hive metadata in an MRS cluster.

Using Metadata Manager
----------------------

Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

-  Viewing metadata of Hive tables

   Click |image1| in the navigation tree on the left and click a table name. The metadata of the Hive table is displayed.

-  Managing metadata of Hive tables

   On the metadata information page of a Hive table:

   -  Click **Import** in the upper right corner to import data.
   -  Click **Overview** to view the location of the table file in the **PROPERTIES** field.
   -  Click **Sample** to browse data.

-  Managing Hive metadata tables

   Click |image2| in the left list to create a table based on the uploaded file in the database. You can also manually create a table.

.. caution::

   The Hue page is used to view and analyze data such as files and tables. Do not perform high-risk management operations such as deleting objects on the page. If an operation is required, you are advised to perform the operation on each component after confirming that the operation has no impact on services. For example, you can use the HDFS client to perform operations on HDFS files and use the Hive client to perform operations on Hive tables.

.. |image1| image:: /_static/images/en-us_image_0000001296219736.png
.. |image2| image:: /_static/images/en-us_image_0000001295900268.png
