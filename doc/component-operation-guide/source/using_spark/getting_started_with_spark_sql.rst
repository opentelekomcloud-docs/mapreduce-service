:original_name: mrs_01_0367.html

.. _mrs_01_0367:

Getting Started with Spark SQL
==============================

Spark provides the Spark SQL language that is similar to SQL to perform operations on structured data. This section describes how to use Spark SQL from scratch. Create a table named **src_data**, write a data record in each row of the table, and store the data in the **mrs_20160907** cluster. Then use SQL statements to query data in the table, and delete the table at last.

.. _mrs_01_0367__sf409cb8b039d45e191bed0dc51e447e3:

Prerequisites
-------------

You have obtained the AK/SK for writing data from an OBS data source to a Spark SQL table. To obtain it, perform as follows:

#. Log in to the management console.
#. Click the username and select **My Credentials** from the drop-down list.
#. On the displayed **My Credentials** page, click **Access Keys**.
#. Click **Create Access Key** to switch to the **Create Access Key** dialog box.
#. Enter the password and verification code in the email, and click **OK** to download the access key. Keep the access key secure.

Procedure
---------

#. Prepare data sources for Spark SQL analysis.

   The sample text file is as follows:

   .. code-block::

      abcd3ghji
      efgh658ko
      1234jjyu9
      7h8kodfg1
      kk99icxz3

#. Upload data to OBS.

   a. Log in to OBS Console.

   b. Choose **Parallel File System** > **Create Parallel File System** to create a file system named **sparksql**.

      **sparksql** is only an example. The file system name must be globally unique. Otherwise, the parallel file system fails to be created.

   c. Click the name of the **sparksql** file system and click **Files**.

   d. Click **Create Folder** to create the **input** folder.

   e. Go to the **input** folder, choose **Upload File** > **add file**, select the local TXT file, and click **Upload**.

#. Log in to the MRS console. In the left navigation pane, choose **Clusters** > **Active Clusters**, and click a cluster name.

#. Import the text file from OBS to HDFS.

   a. Click the **Files** tab.

   b. On the **HDFS File List** tab page, click **Create Folder**, and create a folder named **userinput**.

   c. Go to the **userinput** folder, and click **Import Data**.

   d. Select the OBS and HDFS paths and click **OK**.

      **OBS Path**: **obs://sparksql/input/sparksql-test.txt**

      **HDFS Path**: **/user/userinput**

#. Submit the SQL statement.

   a. On the MRS console, select **Job Management**. For details about how to submit the statement, see `Running a SparkSubmit or Spark Job <https://docs.otc.t-systems.com/en-us/usermanual/mrs/mrs_01_0524.html>`__.

      A job can be submitted only when the **mrs_20160907** cluster is in the **Running** state.

   b. Enter the Spark SQL statement for table creation.

      When entering Spark SQL statements, ensure that the statement characters are not more than 10,000.

      Syntax:

      **CREATE** [EXTERNAL] **TABLE** [IF NOT EXISTS] *table_name* [(col_name data_type [COMMENT col_comment], ...)] [COMMENT table_comment] [PARTITIONED **BY** (col_name data_type [COMMENT col_comment], ...)] [CLUSTERED **BY** (col_name, col_name, ...) [SORTED **BY** (col_name [ASC|DESC], ...)] INTO num_buckets BUCKETS] [ROW FORMAT row_format] [STORED **AS** file_format] [LOCATION hdfs_path];

      You can use the following two methods to create a table example:

      -  Method 1: Create table **src_data** and write data in every row.

         -  The data source is stored in the **/user/userinput** folder of HDFS: **create external table** *src_data\ *\ **(line string) row format delimited fields terminated by '\\\\n' stored as textfile location** '*/user/userinput*';

         -  The data source is stored in the **/sparksql/input** folder of OBS: **create external table** *src_data*\ **(line string) row format delimited fields terminated by '\\\\n' stored as textfile location** '*obs://AK:SK@sparksql/input*';

            For details about how to obtain the AK/SK, see :ref:`Prerequisites <mrs_01_0367__sf409cb8b039d45e191bed0dc51e447e3>`.

      -  Method 2: Create table **src_data1** and load data to the table in batches.

         **create table** *src_data1* **(line string) row format delimited fields terminated by ','** ;

         **load data inpath** '*/user/userinput/sparksql-test.txt*' **into table** *src_data1*;

      .. note::

         When method 2 is used, the data from OBS cannot be loaded to the created tables directly.

   c. Enter the Spark SQL statement for table query.

      Syntax:

      **SELECT** col_name **FROM** *table_name*;

      Example of querying all data in the **src_data** table:

      **select \* from src_data;**

   d. Enter the Spark SQL statement for table deletion.

      Syntax:

      **DROP TABLE** [IF EXISTS] *table_name*;

      Example of deleting the **src_data** table:

      **drop table src_data;**

   e. Click **Check** to check the statement correctness.

   f. Click **OK**.

      After the Spark SQL statements are submitted, the statement execution results are displayed in the result column.

#. Delete the cluster.
