:original_name: mrs_01_1124.html

.. _mrs_01_1124:

Table Input
===========

Overview
--------

**Table Input** operator converts specified columns in a relational database table into input fields of the same quantity.

Input and Output
----------------

-  Input: table columns
-  Output: fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameters description

   +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                            | Type        | Mandatory   | Default Value |
   +==============+========================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | Input fields | Information about relational database input fields:                                                                                                                                                                                                                                                                                                                                                                                                    | map         | Yes         | None          |
   |              |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |              | -  **position**: position of input fields                                                                                                                                                                                                                                                                                                                                                                                                              |             |             |               |
   |              | -  **field name**: input field name                                                                                                                                                                                                                                                                                                                                                                                                                    |             |             |               |
   |              | -  **type**: field type                                                                                                                                                                                                                                                                                                                                                                                                                                |             |             |               |
   |              | -  length: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   +--------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  Fields are generated in a specified order. Table columns to be converted are specified by **From** in step 2 of job configuration. If **Table column names** is set, the value is the table columns to be converted; if **Table column names** is not set, the table columns to be converted are all table columns in the table by default or the columns specified by the query conditions set by **Table SQL statement**.
-  The number of input fields cannot be greater than number of specified columns; otherwise, all data becomes dirty data.
-  If the field value does not match the actual type, the data in the line will become dirty data.

Example
-------

Use SQL Server 2014 as an example. Run the following command to create a **test** table:

**create table test (id int, name text, value text);**

Insert three data lines to the test table:

**insert into test values (1,'zhangshan','zhang');**

**insert into test values (2,'lisi','li');**

**insert into test values (3,'wangwu','wang');**

Query the table:

|image1|

Configure the **Table Input** operator to generate the following fields:

After the data connector is set, click **Automatic Identification**. The system will automatically read fields in the database and select required fields for adding. You only need to optimize or modify the fields manually based on service scenarios.

.. note::

   Performing this operation will overwrite existing data in the table.

|image2|

Configure the output operator to output data to HDFS/OBS. The result is as follows:

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001348740137.jpg
.. |image2| image:: /_static/images/en-us_image_0000001349259405.png
.. |image3| image:: /_static/images/en-us_image_0000001349139825.jpg
