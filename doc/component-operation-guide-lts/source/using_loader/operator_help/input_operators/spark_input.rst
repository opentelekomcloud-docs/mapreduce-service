:original_name: mrs_01_1129.html

.. _mrs_01_1129:

Spark Input
===========

Overview
--------

The **Spark Input** operator converts specified columns in an SparkSQL table into input fields of the same quantity.

Input and Output
----------------

-  Input: SparkSQL table column
-  Output: fields

Parameters
----------

.. table:: **Table 1** Operator parameters description

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                            | Type        | Mandatory   | Default Value |
   +=======================+========================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | Spark database        | Name of a Spark SQL database                                                                                                                                                                                                                                                                                                                                                                                                                           | String      | No          | default       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Spark table name      | Configures the SparkSQL table name.                                                                                                                                                                                                                                                                                                                                                                                                                    | String      | Yes         | None          |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                       | Only one SparkSQL table is supported.                                                                                                                                                                                                                                                                                                                                                                                                                  |             |             |               |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Partition filter      | Configures the partition filter can export data of specific partitions. The parameter is null by default and data of the whole table can be exported.                                                                                                                                                                                                                                                                                                  | String      | No          | ``-``         |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                       | For example, to export data of a table whose partition field's locale value is **CN** or **US**, the input is as follows:                                                                                                                                                                                                                                                                                                                              |             |             |               |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                       | **locale = "CN" or locale = "US"**                                                                                                                                                                                                                                                                                                                                                                                                                     |             |             |               |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Input fields of Spark | Configures the input information of SparkSQL                                                                                                                                                                                                                                                                                                                                                                                                           | map         | Yes         | ``-``         |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                       | -  column name: SparkSQL column name.                                                                                                                                                                                                                                                                                                                                                                                                                  |             |             |               |
   |                       | -  field name: Input field name.                                                                                                                                                                                                                                                                                                                                                                                                                       |             |             |               |
   |                       | -  type: Field type.                                                                                                                                                                                                                                                                                                                                                                                                                                   |             |             |               |
   |                       | -  length: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  If the SparkSQL table name does not exist, the job fails to be submitted.
-  If the configured column names are inconsistent with the SparkSQL table column names, the data cannot be read and the number of imported data records is 0.
-  If the field value does not match the actual type, the data in the line will become dirty data.

**Example**
-----------

Use the data export from Spark to SQL Server 2014 as an example.

In SQL Server 2014, run the following statement to create an empty table **test_1** for storing SparkSQL data. Run the following statement:

**create table test_1 (id int, name text, value text);**

Configure the **Spark Input** operator to generate fields A, B, and C.

After the data connector is set, click **Automatic Identification**. The system will automatically read fields in the database and select required fields for adding. You only need to optimize or modify the fields manually based on service scenarios.

.. note::

   Performing this operation will overwrite existing data in the table.

|image1|

Use the **Table Out** operator to export A, B, and C to the **test_1** table.

**select \* from test_1;**

|image2|

.. |image1| image:: /_static/images/en-us_image_0000001349059721.png
.. |image2| image:: /_static/images/en-us_image_0000001295900036.png
