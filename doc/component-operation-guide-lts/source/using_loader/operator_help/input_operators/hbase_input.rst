:original_name: mrs_01_1125.html

.. _mrs_01_1125:

HBase Input
===========

Overview
--------

The **HBase Input** operator converts specified columns in an HBase table into input fields of the same quantity.

Input and Output
----------------

-  Input: HBase table columns
-  Output: fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameter description

   +--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                | Type        | Mandatory   | Default Value |
   +====================+============================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | Hbase Table Type   | HBase table type. The options include **normal** (common HBase table) and **phoenix**.                                                                                                                                                                                                                                                                                                                                                                     | enum        | Yes         | normal        |
   +--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | HBase table name   | HBase table name. Only one HBase table is supported.                                                                                                                                                                                                                                                                                                                                                                                                       | string      | Yes         | None          |
   +--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | HBase input fields | HBase input information:                                                                                                                                                                                                                                                                                                                                                                                                                                   | map         | Yes         | None          |
   |                    |                                                                                                                                                                                                                                                                                                                                                                                                                                                            |             |             |               |
   |                    | -  **family name**: HBase column family name.                                                                                                                                                                                                                                                                                                                                                                                                              |             |             |               |
   |                    | -  **column name**: HBase column name.                                                                                                                                                                                                                                                                                                                                                                                                                     |             |             |               |
   |                    | -  **field name**: Names of input fields.                                                                                                                                                                                                                                                                                                                                                                                                                  |             |             |               |
   |                    | -  **type**: Field type.                                                                                                                                                                                                                                                                                                                                                                                                                                   |             |             |               |
   |                    | -  **length**: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   |                    | -  **is rowkey**: Indicates whether a column is a primary key column. A common HBase table can have only one primary key, while a phoenix table can have multiple primary keys. If multiple primary keys are configured, they are combined according to the configuration sequence. At least one primary key column must be configured.                                                                                                                    |             |             |               |
   +--------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  If the HBase table name does not exist, the job fails to be submitted.
-  If the configured column names are inconsistent with the HBase table column names, the data cannot be read and the number of imported data records is 0.
-  If the number of input field columns is greater than the number of field columns actually included in the original data, all data becomes dirty data.
-  If the field value does not match the actual type, the data in the line will become dirty data.

Example
-------

Use the data export from HBase to sqlserver2014 as an example.

In sqlserver2014, run the following statement to create an empty data test_1 for storing HBase data:

**create table test_1 (id int, name text, value text);**

Configure the **HBase Input** operator to generate fields A, B, and C.

After the database connection is set up, click **autoRecognition**. The system will automatically read fields in the database and select required fields for adding. You only need to optimize or modify the fields manually based on service scenarios.

.. note::

   Performing this operation will overwrite existing data in the table.

|image1|

Use the **Table Out** operator to export A, B, and C to the test_1 table.

**select \* from test_1;**

|image2|

.. |image1| image:: /_static/images/en-us_image_0000001349139569.png
.. |image2| image:: /_static/images/en-us_image_0000001348739881.jpg
