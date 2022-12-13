:original_name: mrs_01_0386.html

.. _mrs_01_0386:

Using CarbonData from Scratch
=============================

This section is for MRS 3.x or earlier. For MRS 3.x or later, see :ref:`Using CarbonData (for MRS 3.x or Later) <mrs_01_1400>`.

This section describes the procedure of using Spark CarbonData. All tasks are based on the Spark-beeline environment. The tasks include:

#. Connecting to Spark

   Before performing any operation on CarbonData, users must connect CarbonData to Spark.

#. Creating a CarbonData table

   After connecting to Spark, users must create a CarbonData table to load and query data.

#. Loading data to the CarbonData table

   Users load data from CSV files in HDFS to the CarbonData table.

#. Querying data from the CarbonData table

   After data is loaded to the CarbonData table, users can run query commands such as **groupby** and **where**.

Prerequisites
-------------

A client has been installed. For details, see :ref:`Using an MRS Client <mrs_01_2126>`.

Procedure
---------

#. Connect CarbonData to Spark.

   a. Prepare a client based on service requirements and use user **root** to log in to the node where the client is installed.

      For example, if you have updated the client on the Master2 node, log in to the Master2 node to use the client. For details, see :ref:`Using an MRS Client <mrs_01_2126>`.

   b. Run the following commands to switch the user and configure environment variables:

      **sudo su - omm**

      **source /opt/client/bigdata_env**

   c. For clusters with Kerberos authentication enabled, run the following command to authenticate the user. For clusters with Kerberos authentication disabled, skip this step.

      **kinit** **Spark username**

      .. note::

         The user needs to be added to user groups **hadoop** (primary group) and **hive**.

   d. Run the following command to connect to the Spark environment.

      **spark-beeline**

#. Create a CarbonData table.

   Run the following command to create a CarbonData table, which is used to load and query data.

   **CREATE TABLE x1 (imei string, deviceInformationId int, mac string, productdate timestamp, updatetime timestamp, gamePointId double, contractNumber double)**

   **STORED BY 'org.apache.carbondata.format'**

   **TBLPROPERTIES ('DICTIONARY_EXCLUDE'='mac','DICTIONARY_INCLUDE'='deviceInformationId');**

   The command output is as follows:

   .. code-block::

      +---------+--+
      | result  |
      +---------+--+
      +---------+--+
      No rows selected (1.551 seconds)

#. Load data from CSV files to the CarbonData table.

   Run the command to load data from CSV files based on the required parameters. Only CSV files are supported. The CSV column name and sequence configured in the **LOAD** command must be consistent with those in the CarbonData table. The data formats and number of data columns in the CSV files must also be the same as those in the CarbonData table.

   The CSV files must be stored on HDFS. You can upload the files to OBS and import them from OBS to HDFS on the **Files** page of the MRS console.

   If Kerberos authentication is enabled, prepare the CSV files in the work environment and import them to HDFS using open-source HDFS commands. In addition, assign the Spark user with the read and execute permissions of the files on HDFS by referring to :ref:`5 <mrs_01_1406__li122143593123>`.

   For example, the **data.csv** file is saved in the **tmp** directory of HDFS with the following contents:

   .. code-block::

      x123,111,dd,2017-04-20 08:51:27,2017-04-20 07:56:51,2222,33333

   The command for loading data from that file is as follows:

   **LOAD DATA inpath 'hdfs://hacluster/tmp/data.csv' into table x1 options('DELIMITER'=',','QUOTECHAR'='"','FILEHEADER'='imei, deviceinformationid,mac,productdate,updatetime,gamepointid,contractnumber');**

   The command output is as follows:

   .. code-block::

      +---------+--+
      | Result  |
      +---------+--+
      +---------+--+
      No rows selected (3.039 seconds)

#. Query data from the CarbonData.

   -  **Obtaining the number of records**

      Run the following command to obtain the number of records in the CarbonData table:

      **select count(*) from x1;**

   -  **Querying with the groupby condition**

      Run the following command to obtain the **deviceinformationid** records without repetition in the CarbonData table:

      **select deviceinformationid,count (distinct deviceinformationid) from x1 group by deviceinformationid;**

   -  **Querying with the where condition**

      Run the following command to obtain specific **deviceinformationid** records:

      **select \* from x1 where deviceinformationid='111';**

   .. note::

      If the query result has non-English characters, the columns in the query result may not be aligned. This is because characters of different languages occupy different widths.

#. Run the following command to exit the Spark environment.

   **!quit**
