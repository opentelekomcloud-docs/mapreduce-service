:original_name: mrs_01_0372.html

.. _mrs_01_0372:

Using the Metadata Browser on the Hue Web UI
============================================

Scenario
--------

Users can use the Hue web UI to manage Hive metadata in an MRS cluster.

For versions earlier than MRS 1.9.2, MRS clusters with Kerberos authentication enabled support this function.

Using Metastore Manager
-----------------------

Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0370>`.

Choose **Data Browsers** > **Metastore Tables**, and access **Metastore Manager**.

-  Viewing metadata of Hive tables

   In the left navigation pane, move the cursor to a table and click |image1| on the right. The metadata of the Hive table is displayed.

-  Managing metadata of Hive tables

   On the metadata page of a Hive table, you can click |image2| in the upper right corner to import data, click |image3| to browse data, and click |image4| to view the location of the table file.

   .. caution::

      The Hue page is used to view and analyze data such as files and tables. Do not perform high-risk management operations such as deleting objects on the page. If an operation is required, you are advised to perform the operation on each component after confirming that the operation has no impact on services. For example, you can use the HDFS client to perform operations on HDFS files and use the Hive client to perform operations on Hive tables.

-  Managing Hive metadata tables

   Click |image5| in the upper right corner to create a table in the database based on the uploaded files. Or click |image6| in the upper right corner to manually create a table.

Accessing Metastore Manager
---------------------------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0370>`.

#. Choose **Data Browsers** > **Metastore Tables**, and access **Metastore Manager**.

   **Metastore Manager** supports the following functions:

   -  Creating a Hive table from a file
   -  Manually creating a Hive table
   -  Viewing Hive table metadata

Creating a Hive table from a File
---------------------------------

#. Access **Metastore Manager** and select a database in **Databases**.

   The default database is **default**.

#. Click |image7|. The **Create a new table from a file** page is displayed.

#. Select a file.

   a. In **Table Name**, enter a Hive table name.

      A Hive table name contains no more than 128 characters, including letters, numbers, or underscores (_), and must start with a letter or number.

   b. In **Description**, enter description about the Hive table as required.

   c. In **Input File or Location**, click |image8| and select a Hive table file from HDFS. The file is used to store new data of the Hive table.

      If the file is not stored in HDFS, click **Upload a file** to upload the file from the local directory to HDFS. Multiple files can be simultaneously uploaded. The files cannot be empty.

   d. If you need to import the data in the file to the Hive table, select **Import data** as **Load method**. By default, **Import data** is selected.

      If you select **Create External Table**, a Hive external table is created.

      .. note::

         If you select **Create External Table**, set **Input File or Location** to a path.

      If you select **Leave Empty**, an empty Hive table is created.

   e. Click **Next**.

#. Set a delimiter.

   a. In **Delimiter**, select one.

      If your desired delimiter is not in the list, select **Other..** and enter a delimiter.

   b. Click **Preview** to preview data processing.

   c. Click **Next**.

#. Define a column.

   a. If you click |image9| on the right side of **Use first row as column names**, the first row of data in the file is used as a column name. If you do not click it, the first row of data is not used as the column name.

   b. In **Column name**, set a name for each column.

      A Hive table name contains no more than 128 characters, including letters, numbers, or underscores (_), and must start with a letter or number.

      .. note::

         You can rename columns in batches by clicking |image10| on the right side of **Bulk edit column names**. Enter all column names and separate them by commas (,).

   c. In **Column Type**, select a type for each column.

#. Click **Create Table** to create the table. Wait for Hue to display information about the Hive table.

Manually Creating a Hive Table
------------------------------

#. Access **Metastore Manager** and select a database in **Databases**.

   The default database is **default**.

#. Click |image11|. The **Create a new table manually** page is displayed.

#. Set a table name.

   a. In **Table Name**, enter a Hive table name.

      A Hive table name contains no more than 128 characters, including letters, numbers, or underscores (_), and must start with a letter or number.

   b. In **Description**, enter description about the Hive table as required.

   c. Click **Next**.

#. Select a data storage format.

   -  If data needs to be separated by delimiters, select **Delimited** and perform :ref:`5 <mrs_01_0372__li379246041509>`.
   -  If data needs to be stored in serialization format, select **SerDe** and perform :ref:`6 <mrs_01_0372__li119336551509>`.

#. .. _mrs_01_0372__li379246041509:

   Set a delimiter.

   a. In **Field terminator**, set a column delimiter.

      If your desired delimiter is not in the list, select **Other..** and enter a delimiter.

   b. In **Collection terminator**, set a delimiter to separate the data set of columns of the **array** type in Hive. For example, the type of a column is array. A value needs to store **employee** and **manager**. The user specifies a colon (**:**) as the delimiter. Therefore, the final value is **employee:manager**.

   c. In **Map key terminator**, set a delimiter to separate the data set of columns of the **map** type in Hive. For example, the type of a column is map. A value needs to store **home** of **aaa** and **company** of **bbb**. The user defines **\|** as the delimiter. Therefore, the final value is **home|aaa:company|bbb**.

   d. Click **Next** and perform :ref:`7 <mrs_01_0372__li564987691509>`.

#. .. _mrs_01_0372__li119336551509:

   Set serialization properties.

   a. In **SerDe Name**, enter the class name of the serialization format: **org.apache.hadoop.hive.serde2.lazy.LazySimpleSerDe**

      Users can expand Hive to support more customized serialization classes.

   b. In **Serde properties**, enter the value of the serialization format: **"field.delim"="," "colelction.delim"=":" "mapkey.delim"="|"**

   c. Click **Next** and perform :ref:`7 <mrs_01_0372__li564987691509>`.

#. .. _mrs_01_0372__li564987691509:

   Select a data table format and click **Next**.

   -  **TextFile**: indicates that data is stored in text files.

   -  **SequenceFile**: indicates that data is stored in binary files.

   -  **InputFormat**: indicates that data in files is used in the customized input and output formats.

      Users can expand Hive to support more customized formatting classes.

      a. In **InputFormat Class**, enter the class used by input data: **org.apache.hadoop.hive.ql.io.RCFileInputFormat**
      b. In **OutputFormat Class**, enter the class used by output data: **org.apache.hadoop.hive.ql.io.RCFileOutputFormat**

#. Select a file storage location and click **Next**.

   **Use default location** is selected by default. If you want to customize a storage location, deselect the default value and specify a file storage location in **External location** by clicking |image12|.

#. Set columns of the Hive table.

   a. In **Column name**, set a column name.

      A Hive table name contains no more than 128 characters, including letters, numbers, or underscores (_), and must start with a letter or number.

   b. In **Column type**, select a type for each column.

      Click **Add a column** to add a new column.

   c. Click **Add a partition** to add a new partition for the Hive table to improve the query efficiency.

#. Click **Create Table** to create a new table. Wait for Hue to display information about the Hive table.

Managing the Hive Table
-----------------------

#. Access **Metastore Manager** and select a database in **Databases**. All tables in the database are displayed on the page.

   The default database is **default**.

#. Click a table name in the database to view table details.

   The following operations are supported: importing data, browsing data,, or viewing file storage location. When viewing all tables in the database, you can select tables and perform the following operations such as viewing tables and browsing data.

   .. caution::

      The Hue page is used to view and analyze data such as files and tables. Do not perform high-risk management operations such as deleting objects on the page. If an operation is required, you are advised to perform the operation on each component after confirming that the operation has no impact on services. For example, you can use the HDFS client to perform operations on HDFS files and use the Hive client to perform operations on Hive tables.

.. |image1| image:: /_static/images/en-us_image_0000001295930292.png
.. |image2| image:: /_static/images/en-us_image_0000001295770328.png
.. |image3| image:: /_static/images/en-us_image_0000001349169853.png
.. |image4| image:: /_static/images/en-us_image_0000001349289433.png
.. |image5| image:: /_static/images/en-us_image_0000001349169861.png
.. |image6| image:: /_static/images/en-us_image_0000001295770332.png
.. |image7| image:: /_static/images/en-us_image_0000001349289429.jpg
.. |image8| image:: /_static/images/en-us_image_0000001349169857.jpg
.. |image9| image:: /_static/images/en-us_image_0000001296249764.jpg
.. |image10| image:: /_static/images/en-us_image_0000001348770157.jpg
.. |image11| image:: /_static/images/en-us_image_0000001295930296.jpg
.. |image12| image:: /_static/images/en-us_image_0000001349289425.jpg
