:original_name: mrs_01_1146.html

.. _mrs_01_1146:

Hive output
===========

Overview
--------

The **Hive Output** operator exports existing fields to specified columns of a Hive table.

Input and Output
----------------

-  Input: fields to be exported
-  Output: Hive table

Parameters
----------

.. table:: **Table 1** Operator parameters description

   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                            | Node Type   | Mandatory   | Default Value |
   +==============================+========================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | Hive file storage format     | Hive configuration file storage format. CSV, ORC, and RC are supported at present.                                                                                                                                                                                                                                                                                                                                                                     | enum        | Yes         | CSV           |
   |                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                              | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                              |             |             |               |
   |                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                              |    -  Parquet is a column-based storage format. In this format, the output field names of Loader be the same as the field names in Hive tables.                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                              |    -  For Hive of versions later than 1.2.0, a field name, instead of field number, is used to parse ORC files. Therefore, the output field names of Loader must be the same as those in Hive tables.                                                                                                                                                                                                                                                  |             |             |               |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Hive file compression format | Hive table file compression format. Select a format from the drop-down list. If you select **NONE** or do not set this parameter, data is not compressed.                                                                                                                                                                                                                                                                                              | enum        | Yes         | NONE          |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Hive ORC file version        | Version of the ORC file (when the storage format of the Hive table file is ORC).                                                                                                                                                                                                                                                                                                                                                                       | enum        | Yes         | 0.12          |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Output delimiter             | Delimiter.                                                                                                                                                                                                                                                                                                                                                                                                                                             | string      | Yes         | None.         |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Output fields                | Information about output fields:                                                                                                                                                                                                                                                                                                                                                                                                                       | map         | Yes         | None          |
   |                              |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                              | -  position: Position of output fields.                                                                                                                                                                                                                                                                                                                                                                                                                |             |             |               |
   |                              | -  field name: Names of output fields.                                                                                                                                                                                                                                                                                                                                                                                                                 |             |             |               |
   |                              | -  type: Field type. If type is set to **DATE**, **TIME**, or **TIMESTAMP**, you must specify a time format. If type is set to other values, the time format is invalid. An example time format is **yyyyMMdd HH:mm:ss**.                                                                                                                                                                                                                              |             |             |               |
   |                              | -  decimal format: scale and precision of the decimal.                                                                                                                                                                                                                                                                                                                                                                                                 |             |             |               |
   |                              | -  length: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   |                              | -  partition key: indicates whether a column is a partition column. You can specify zero or multiple partition columns. If multiple primary keys are configured, they are combined according to the configuration sequence.                                                                                                                                                                                                                            |             |             |               |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  The field values are exported to the Hive table.
-  If one or more columns are specified as partition columns, the **Partition Handlers** feature is displayed on the **To** page in Step 4 of the job configuration. **Partition Handlers** specifies the number of handlers for processing data partitioning.
-  If no column is designated as partition columns, input data does not need to be partitioned, and **Partition Handlers** is hidden by default.

Example
-------

Use the **CSV File Input** operator to generate two fields A and B.

The following figure shows the source file.

|image1|

Configure the **Hive Output** operator to export a_str and b_str to the Hive table.

|image2|

After the execution is complete, view the table data.

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001348739729.jpg
.. |image2| image:: /_static/images/en-us_image_0000001349139421.png
.. |image3| image:: /_static/images/en-us_image_0000001388325592.png
