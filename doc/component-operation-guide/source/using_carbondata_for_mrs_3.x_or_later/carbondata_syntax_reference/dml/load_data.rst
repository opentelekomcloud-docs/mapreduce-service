:original_name: mrs_01_1438.html

.. _mrs_01_1438:

LOAD DATA
=========

Function
--------

This command is used to load user data of a particular type, so that CarbonData can provide good query performance.

.. note::

   Only the raw data on HDFS can be loaded.

Syntax
------

**LOAD DATA** *INPATH 'folder_path' INTO TABLE [db_name.]table_name OPTIONS(property_name=property_value, ...);*

Parameter Description
---------------------

.. table:: **Table 1** LOAD DATA parameters

   +-------------+----------------------------------------------------------------------------------+
   | Parameter   | Description                                                                      |
   +=============+==================================================================================+
   | folder_path | Path of the file or folder used for storing the raw CSV data.                    |
   +-------------+----------------------------------------------------------------------------------+
   | db_name     | Database name. If this parameter is not specified, the current database is used. |
   +-------------+----------------------------------------------------------------------------------+
   | table_name  | Name of a table in a database.                                                   |
   +-------------+----------------------------------------------------------------------------------+

Precautions
-----------

The following configuration items are involved during data loading:

-  **DELIMITER**: Delimiters and quote characters provided in the load command. The default value is a comma (**,**).

   *OPTIONS('DELIMITER'=',' , 'QUOTECHAR'='"')*

   You can use **'DELIMITER'='\\t'** to separate CSV data using tabs.

   OPTIONS('DELIMITER'='\\t')

   CarbonData also supports **\\001** and **\\017** as delimiters.

   .. note::

      When the delimiter of CSV data is a single quotation mark ('), the single quotation mark must be enclosed in double quotation marks (" "). For example, 'DELIMITER'= "'".

-  **QUOTECHAR**: Delimiters and quote characters provided in the load command. The default value is double quotation marks (**"**).

   *OPTIONS('DELIMITER'=',' , 'QUOTECHAR'='"')*

-  **COMMENTCHAR**: Comment characters provided in the load command. During data loading, if there is a comment character at the beginning of a line, the line is regarded as a comment line and data in the line will not be loaded. The default value is a pound key (#).

   *OPTIONS('COMMENTCHAR'='#')*

-  **FILEHEADER**: If the source file does not contain any header, add a header to the **LOAD DATA** command.

   *OPTIONS('FILEHEADER'='column1,column2')*

-  **ESCAPECHAR**: Is used to perform strict verification of the escape character on CSV files. The default value is backslash (**\\**).

   OPTIONS('ESCAPECHAR'='\\')

   .. note::

      Enter **ESCAPECHAR** in the CSV data. **ESCAPECHAR** must be enclosed in double quotation marks (" "). For example, "a\\b".

-  .. _mrs_01_1438__lcf623574402c443e908646591898c2be:

   Bad records handling:

   In order for the data processing application to provide benefits, certain data integration is required. In most cases, data quality problems are caused by data sources.

   Methods of handling bad records are as follows:

   -  Load all of the data before dealing with the errors.
   -  Clean or delete bad records before loading data or stop the loading when bad records are found.

   There are many options for clearing source data during CarbonData data loading, as listed in :ref:`Table 2 <mrs_01_1438__t1d4d77614e2b4b92b0f334d52702013b>`.

   .. _mrs_01_1438__t1d4d77614e2b4b92b0f334d52702013b:

   .. table:: **Table 2** Bad Records Logger

      +---------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Configuration Item        | Default Value         | Description                                                                                                                                                                                                                                          |
      +===========================+=======================+======================================================================================================================================================================================================================================================+
      | BAD_RECORDS_LOGGER_ENABLE | false                 | Whether to create logs with details about bad records                                                                                                                                                                                                |
      +---------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | BAD_RECORDS_ACTION        | FAIL                  | The four types of actions for bad records are as follows:                                                                                                                                                                                            |
      |                           |                       |                                                                                                                                                                                                                                                      |
      |                           |                       | -  **FORCE**: Auto-corrects the data by storing the bad records as NULL.                                                                                                                                                                             |
      |                           |                       | -  **REDIRECT**: Bad records are written to the raw CSV instead of being loaded.                                                                                                                                                                     |
      |                           |                       | -  **IGNORE**: Bad records are neither loaded nor written to the raw CSV.                                                                                                                                                                            |
      |                           |                       | -  **FAIL**: Data loading fails if any bad records are found.                                                                                                                                                                                        |
      |                           |                       |                                                                                                                                                                                                                                                      |
      |                           |                       |    .. note::                                                                                                                                                                                                                                         |
      |                           |                       |                                                                                                                                                                                                                                                      |
      |                           |                       |       In loaded data, if all records are bad records, **BAD_RECORDS_ACTION** is invalid and the load operation fails.                                                                                                                                |
      +---------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | IS_EMPTY_DATA_BAD_RECORD  | false                 | Whether empty data of a column to be considered as bad record or not. If this parameter is set to **false**, empty data ("",', or,) is not considered as bad records. If this parameter is set to **true**, empty data is considered as bad records. |
      +---------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | BAD_RECORD_PATH           | ``-``                 | HDFS path where bad records are stored. The default value is **Null**. If bad records logging or bad records operation redirection is enabled, the path must be configured by the user.                                                              |
      +---------------------------+-----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   Example:

   **LOAD DATA INPATH** *'filepath.csv'* **INTO TABLE** *tablename* *OPTIONS('BAD_RECORDS_LOGGER_ENABLE'='true',* *'BAD_RECORD_PATH'='hdfs://hacluster/tmp/carbon', 'BAD_RECORDS_ACTION'='REDIRECT', 'IS_EMPTY_DATA_BAD_RECORD'='false');*

   .. note::

      If **REDIRECT** is used, CarbonData will add all bad records into a separate CSV file. However, this file must not be used for subsequent data loading because the content may not exactly match the source record. You must clean up the source record for further data ingestion. This option is used to remind you which records are bad.

-  **MAXCOLUMNS**: (Optional) Specifies the maximum number of columns parsed by a CSV parser in a line.

   *OPTIONS('MAXCOLUMNS'='400')*

   .. table:: **Table 3** MAXCOLUMNS

      ============================== ============= =============
      Name of the Optional Parameter Default Value Maximum Value
      ============================== ============= =============
      MAXCOLUMNS                     2000          20000
      ============================== ============= =============

   .. table:: **Table 4** Behavior chart of MAXCOLUMNS

      +-------------------------------+--------------------------------------+-----------------------------------------------------------------------------+
      | MAXCOLUMNS Value              | Number of Columns in the File Header | Final Value Considered                                                      |
      +===============================+======================================+=============================================================================+
      | Not specified in Load options | 5                                    | 2000                                                                        |
      +-------------------------------+--------------------------------------+-----------------------------------------------------------------------------+
      | Not specified in Load options | 6000                                 | 6000                                                                        |
      +-------------------------------+--------------------------------------+-----------------------------------------------------------------------------+
      | 40                            | 7                                    | Max (column count of file header, MAXCOLUMNS value)                         |
      +-------------------------------+--------------------------------------+-----------------------------------------------------------------------------+
      | 22000                         | 40                                   | 20000                                                                       |
      +-------------------------------+--------------------------------------+-----------------------------------------------------------------------------+
      | 60                            | Not specified in Load options        | Max (Number of columns in the first line of the CSV file, MAXCOLUMNS value) |
      +-------------------------------+--------------------------------------+-----------------------------------------------------------------------------+

   .. note::

      There must be sufficient executor memory for setting the maximum value of **MAXCOLUMNS Option**. Otherwise, data loading will fail.

-  If **SORT_SCOPE** is set to **GLOBAL_SORT** during table creation, you can specify the number of partitions to be used when sorting data. If this parameter is not set or is set to a value less than **1**, the number of map tasks is used as the number of reduce tasks. It is recommended that each reduce task process 512 MB to 1 GB data.

   *OPTIONS('GLOBAL_SORT_PARTITIONS'='2')*

   .. note::

      To increase the number of partitions, you may need to increase the value of **spark.driver.maxResultSize**, as the sampling data collected in the driver increases with the number of partitions.

-  **DATEFORMAT**: Specifies the date format of the table.

   *OPTIONS('DATEFORMAT'='dateFormat')*

   .. note::

      Date formats are specified by date pattern strings. The date pattern letters in Carbon are same as in JAVA.

-  **TIMESTAMPFORMAT**: Specifies the timestamp of a table.
-  *OPTIONS('TIMESTAMPFORMAT'='timestampFormat')*

-  **SKIP_EMPTY_LINE**: Ignores empty rows in the CSV file during data loading.

   *OPTIONS('SKIP_EMPTY_LINE'='TRUE/FALSE')*

-  **Optional:** **SCALE_FACTOR**: Used to control the number of partitions for **RANGE_COLUMN**, **SCALE_FACTOR**. The formula is as follows:

   .. code-block:: text

      splitSize = max(blocklet_size, (block_size - blocklet_size)) * scale_factor
      numPartitions = total size of input data / splitSize

   The default value is **3**. The value ranges from **1** to **300**.

   *OPTIONS('SCALE_FACTOR'='10')*

   .. note::

      -  If **GLOBAL_SORT_PARTITIONS** and **SCALE_FACTOR** are used at the same time, only **GLOBAL_SORT_PARTITIONS** is valid.
      -  The compaction on **RANGE_COLUMN** will use **LOCAL_SORT** by default.

Scenarios
---------

To load a CSV file to a CarbonData table, run the following statement:

**LOAD DATA** *INPATH 'folder path' INTO TABLE tablename OPTIONS(property_name=property_value, ...);*

Examples
--------

The data in the **data.csv** file is as follows:

.. code-block::

   ID,date,country,name,phonetype,serialname,salary
   4,2014-01-21 00:00:00,city1,aaa4,phone2435,ASD66902,15003
   5,2014-01-22 00:00:00,city1,aaa5,phone2441,ASD90633,15004
   6,2014-03-07 00:00:00,city1,aaa6,phone294,ASD59961,15005

CREATE TABLE carbontable(ID int, date Timestamp, country String, name String, phonetype String, serialname String,salary int) STORED AS carbondata;

**LOAD DATA** *inpath 'hdfs://hacluster/tmp/data.csv' INTO table carbontable*

*options('DELIMITER'=',');*

System Response
---------------

Success or failure will be recorded in the driver logs.
