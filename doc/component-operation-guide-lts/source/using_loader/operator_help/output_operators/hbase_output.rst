:original_name: mrs_01_1150.html

.. _mrs_01_1150:

HBase Output
============

Overview
--------

The **HBase Output** operator exports existing fields to specified columns of an HBase Outputtable.

Input and Output
----------------

-  Input: fields to be exported
-  Output: HBase table

Parameters
----------

.. table:: **Table 1** Operator parameters description

   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+------------------------------------+
   | Parameter                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                            | Node Type   | Mandatory   | Default Value                      |
   +============================+========================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+====================================+
   | HBase table type           | HBase table type. The options include normal (common HBase table) and phoenix.                                                                                                                                                                                                                                                                                                                                                                         | enum        | Yes         | normal                             |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+------------------------------------+
   | NULL value processing mode | Null value processing mode. Selecting the option button indicates to convert null values to empty strings and save them. Deselecting the option button indicates the data is not saved.                                                                                                                                                                                                                                                                | boolean     | No          | The option button is not selected. |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+------------------------------------+
   | HBase output fields        | HBase output information:                                                                                                                                                                                                                                                                                                                                                                                                                              | map         | Yes         | None                               |
   |                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |                                    |
   |                            | -  field name: Names of output fields.                                                                                                                                                                                                                                                                                                                                                                                                                 |             |             |                                    |
   |                            | -  table name: HBase table name.                                                                                                                                                                                                                                                                                                                                                                                                                       |             |             |                                    |
   |                            | -  family name: HBase column family name.                                                                                                                                                                                                                                                                                                                                                                                                              |             |             |                                    |
   |                            | -  column name: HBase column name.                                                                                                                                                                                                                                                                                                                                                                                                                     |             |             |                                    |
   |                            | -  type: Field type. If type is set to **DATE**, **TIME**, or **TIMESTAMP**, you must specify a time format. If type is set to other values, the time format is invalid. An example time format is **yyyyMMdd HH:mm:ss**.                                                                                                                                                                                                                              |             |             |                                    |
   |                            | -  length: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |                                    |
   |                            | -  Primary Key: Indicates whether a column is a primary key column. A common HBase table can have only one primary key, while a phoenix table can have multiple primary keys. If multiple primary keys are configured, they are combined according to the configuration sequence. At least one primary key column must be configured.                                                                                                                  |             |             |                                    |
   +----------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+------------------------------------+

Data Processing Rule
--------------------

-  The field values are exported to the HBase table.
-  When the original data contains NULL values, if the **NULL value processing mode** is selected, the NULL values are converted to empty strings and saved. If the **NULL value processing mode** button is not selected, the data is not saved.

Example
-------

Using table input as an example, after the fields are generated, the HBase Output operator exports them to the related HBase table and stores the data in the test table, as shown in the following figure.

|image1|

Create an HBase table.

**create 'hbase_test','f1','f2';**

Configure the **HBase Output** operator, as shown in the following figure.

|image2|

After the job execution is complete, view the data in the hbase_test table.

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001296219468.jpg
.. |image2| image:: /_static/images/en-us_image_0000001296059836.png
.. |image3| image:: /_static/images/en-us_image_0000001295740028.jpg
