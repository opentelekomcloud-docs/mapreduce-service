:original_name: mrs_01_1128.html

.. _mrs_01_1128:

Hive input
==========

Overview
--------

The **Hive Input** operator converts specified columns in an HBase table into input fields of the same quantity.

Input and Output
----------------

-  Input: Hive table columns
-  Output: fields

Parameters
----------

.. table:: **Table 1** Operator parameters description

   +------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                            | Node Type   | Mandatory   | Default Value |
   +==================+========================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | Hive database    | Name of a Hive database                                                                                                                                                                                                                                                                                                                                                                                                                                | String      | No          | default       |
   +------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Hive table name  | Name of the Hive table configured                                                                                                                                                                                                                                                                                                                                                                                                                      | String      | Yes         | None.         |
   |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                  | Only one Hive table is supported.                                                                                                                                                                                                                                                                                                                                                                                                                      |             |             |               |
   +------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Partition filter | Configures the partition filter can export data of specific partitions. The parameter is null by default and data of the whole table can be exported.                                                                                                                                                                                                                                                                                                  | String      | No          | ``-``         |
   |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                  | For example, to export data of a table whose partition field's locale value is **CN** or **US**, the input is as follows:                                                                                                                                                                                                                                                                                                                              |             |             |               |
   |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                  | **locale = "CN" or locale = "US"**                                                                                                                                                                                                                                                                                                                                                                                                                     |             |             |               |
   +------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Hive input field | Configures the input information of Hive                                                                                                                                                                                                                                                                                                                                                                                                               | map         | Yes         | ``-``         |
   |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                  | -  column name: Hive column name.                                                                                                                                                                                                                                                                                                                                                                                                                      |             |             |               |
   |                  | -  field name: Input field name.                                                                                                                                                                                                                                                                                                                                                                                                                       |             |             |               |
   |                  | -  type: Field type.                                                                                                                                                                                                                                                                                                                                                                                                                                   |             |             |               |
   |                  | -  length: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   +------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  If the Hive table name does not exist, the job fails to be submitted.
-  If the configured column names are inconsistent with the Hive table column names, the data cannot be read and the number of imported data records is 0.
-  If the field value does not match the actual type, the data in the line will become dirty data.

Example
-------

Use the data export from Hive to SQL Server 2014 as an example.

In SQL Server 2014, run the following statement to create an empty table **test_1** for storing Hive data. Run the following statement:

**create table test_1 (id int, name text, value text);**

Configure the **Hive Input** operator to generate fields A, B, and C.

After the data connector is set, click **Automatic Identification**. The system will automatically read fields in the database and select required fields for adding. You only need to optimize or modify the fields manually based on service scenarios.

.. note::

   Performing this operation will overwrite existing data in the table.

|image1|

Use the **Table Out** operator to export A, B, and C to the **test_1** table.

**select \* from test_1;**

|image2|

.. |image1| image:: /_static/images/en-us_image_0000001349259305.png
.. |image2| image:: /_static/images/en-us_image_0000001295900168.png
