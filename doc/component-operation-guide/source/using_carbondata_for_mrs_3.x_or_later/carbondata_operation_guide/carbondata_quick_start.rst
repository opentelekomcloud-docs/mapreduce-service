:original_name: mrs_01_1406.html

.. _mrs_01_1406:

CarbonData Quick Start
======================

This section describes how to create CarbonData tables, load data, and query data. This quick start provides operations based on the Spark Beeline client. If you want to use Spark shell, wrap the queries with **spark.sql()**.

**The following describes how to load data from a CSV file to a CarbonData table**.

.. table:: **Table 1** CarbonData Quick Start

   +-----------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | Operation                                                                                     | Description                                                           |
   +===============================================================================================+=======================================================================+
   | :ref:`Preparing a CSV File <mrs_01_1406__section497653817420>`                                | Prepare the CSV file to be loaded to the CarbonData Table.            |
   +-----------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`Connecting to CarbonData <mrs_01_1406__s2af9b9318a0f44c48f3b0fa8217a12fe>`              | Connect to CarbonData before performing any operations on CarbonData. |
   +-----------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`Creating a CarbonData Table <mrs_01_1406__sffd808b54dab44fc8613a01cc8e39baf>`           | Create a CarbonData table to load data and perform query operations.  |
   +-----------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`Loading Data to a CarbonData Table <mrs_01_1406__s79b594787a2a46819cf07478d4a0d81c>`    | Load data from CSV to the created table.                              |
   +-----------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+
   | :ref:`Querying Data from a CarbonData Table <mrs_01_1406__s68e9413d1b234b2d91557a1739fc7828>` | Perform query operations such as filters and groupby.                 |
   +-----------------------------------------------------------------------------------------------+-----------------------------------------------------------------------+

.. _mrs_01_1406__section497653817420:

Preparing a CSV File
--------------------

#. Prepare a CSV file named **test.csv** on the local PC. An example is as follows:

   .. code-block::

      13418592122,1001, MAC address, 2017-10-23 15:32:30,2017-10-24 15:32:30,62.50,74.56
      13418592123 1002,  MAC address, 2017-10-23 16:32:30,2017-10-24 16:32:30,17.80,76.28
      13418592124,1003, MAC address, 2017-10-23 17:32:30,2017-10-24 17:32:30,20.40,92.94
      13418592125 1004,  MAC address, 2017-10-23 18:32:30,2017-10-24 18:32:30,73.84,8.58
      13418592126,1005, MAC address, 2017-10-23 19:32:30,2017-10-24 19:32:30,80.50,88.02
      13418592127 1006,  MAC address, 2017-10-23 20:32:30,2017-10-24 20:32:30,65.77,71.24
      13418592128,1007, MAC address, 2017-10-23 21:32:30,2017-10-24 21:32:30,75.21,76.04
      13418592129,1008, MAC address, 2017-10-23 22:32:30,2017-10-24 22:32:30,63.30,94.40
      13418592130, 1009, MAC address, 2017-10-23 23:32:30,2017-10-24 23:32:30,95.51,50.17
      13418592131,1010, MAC address, 2017-10-24 00:32:30,2017-10-25 00:32:30,39.62,99.13

#. Use WinSCP to import the CSV file to the directory of the node where the client is installed, for example, **/opt**.

#. Log in to FusionInsight Manager and choose **System**. In the navigation pane on the left, choose **Permission** > **User**, click **Create** to create human-machine user **sparkuser**, and add the user to user groups hadoop (primary group) and hive.

#. Run the following commands to go to the client installation directory, load environment variables, and authenticate the user.

   **cd /**\ *Client installation directory*

   **source ./bigdata_env**

   **source ./Spark2x/component_env**

   **kinit sparkuser**

#. .. _mrs_01_1406__li122143593123:

   Run the following command to upload the CSV file to the **/data** directory of the HDFS.

   **hdfs dfs -put /opt/test.csv /data/**

.. _mrs_01_1406__s2af9b9318a0f44c48f3b0fa8217a12fe:

Connecting to CarbonData
------------------------

-  Use Spark SQL or Spark shell to connect to Spark and run Spark SQL commands.

-  Run the following commands to start the JDBCServer and use a JDBC client (for example, Spark Beeline) to connect to the JDBCServer.

   **cd ./Spark2x/spark/bin**

   **./spark-beeline**

.. _mrs_01_1406__sffd808b54dab44fc8613a01cc8e39baf:

Creating a CarbonData Table
---------------------------

After connecting Spark Beeline with the JDBCServer, create a CarbonData table to load data and perform query operations. Run the following commands to create a simple table:

**create table x1 (imei string, deviceInformationId int, mac string, productdate timestamp, updatetime timestamp, gamePointId double, contractNumber double) STORED AS carbondata TBLPROPERTIES ('SORT_COLUMNS'='imei,mac');**

The command output is as follows:

.. code-block::

   +---------+
   | Result  |
   +---------+
   +---------+
   No rows selected (1.093 seconds)

.. _mrs_01_1406__s79b594787a2a46819cf07478d4a0d81c:

Loading Data to a CarbonData Table
----------------------------------

After you have created a CarbonData table, you can load the data from CSV to the created table.

Run the following command with required parameters to load data from CSV. The column names of the CarbonData table must match the column names of the CSV file.

**LOAD DATA inpath 'hdfs://hacluster/data/**\ *test.csv*\ **' into table** *x1* **options('DELIMITER'=',', 'QUOTECHAR'='"','FILEHEADER'='imei, deviceinformationid,mac, productdate,updatetime, gamepointid,contractnumber');**

**test.csv** is the CSV file prepared in :ref:`Preparing a CSV File <mrs_01_1406__section497653817420>` and **x1** is the table name.

The CSV example file is as follows:

.. code-block::

   13418592122,1001, MAC address, 2017-10-23 15:32:30,2017-10-24 15:32:30,62.50,74.56
   13418592123 1002,  MAC address, 2017-10-23 16:32:30,2017-10-24 16:32:30,17.80,76.28
   13418592124,1003, MAC address, 2017-10-23 17:32:30,2017-10-24 17:32:30,20.40,92.94
   13418592125 1004,  MAC address, 2017-10-23 18:32:30,2017-10-24 18:32:30,73.84,8.58
   13418592126,1005, MAC address, 2017-10-23 19:32:30,2017-10-24 19:32:30,80.50,88.02
   13418592127 1006,  MAC address, 2017-10-23 20:32:30,2017-10-24 20:32:30,65.77,71.24
   13418592128,1007, MAC address, 2017-10-23 21:32:30,2017-10-24 21:32:30,75.21,76.04
   13418592129,1008, MAC address, 2017-10-23 22:32:30,2017-10-24 22:32:30,63.30,94.40
   13418592130, 1009, MAC address, 2017-10-23 23:32:30,2017-10-24 23:32:30,95.51,50.17
   13418592131,1010, MAC address, 2017-10-24 00:32:30,2017-10-25 00:32:30,39.62,99.13

The command output is as follows:

.. code-block::

   +------------+
   |Segment ID  |
   +------------+
   |0           |
   +------------+
   No rows selected (3.039 seconds)

.. _mrs_01_1406__s68e9413d1b234b2d91557a1739fc7828:

Querying Data from a CarbonData Table
-------------------------------------

After a CarbonData table is created and the data is loaded, you can perform query operations as required. Some query operations are provided as examples.

-  **Obtaining the number of records**

   Run the following command to obtain the number of records in the CarbonData table:

   **select count(*) from x1;**

-  **Querying with the groupby condition**

   Run the following command to obtain the **deviceinformationid** records without repetition in the CarbonData table:

   **select deviceinformationid,count (distinct deviceinformationid) from x1 group by deviceinformationid;**

-  **Querying with Filter**

   Run the following command to obtain specific **deviceinformationid** records:

   **select \* from x1 where deviceinformationid='1010';**

.. note::

   If the query result has non-English characters, the columns in the query result may not be aligned. This is because characters of different languages occupy different widths.

Using CarbonData on Spark-shell
-------------------------------

If you need to use CarbonData on a Spark-shell, you need to create a CarbonData table, load data to the CarbonData table, and query data in CarbonData as follows:

.. code-block::

   spark.sql("CREATE TABLE x2(imei string, deviceInformationId int, mac string, productdate timestamp, updatetime timestamp, gamePointId double, contractNumber double) STORED AS carbondata")
   spark.sql("LOAD DATA inpath 'hdfs://hacluster/data/x1_without_header.csv' into table x2 options('DELIMITER'=',', 'QUOTECHAR'='\"','FILEHEADER'='imei, deviceinformationid,mac, productdate,updatetime, gamepointid,contractnumber')")
   spark.sql("SELECT * FROM x2").show()
