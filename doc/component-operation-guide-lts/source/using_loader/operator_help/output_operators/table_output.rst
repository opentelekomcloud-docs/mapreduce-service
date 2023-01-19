:original_name: mrs_01_1148.html

.. _mrs_01_1148:

Table Output
============

Overview
--------

The **Table Output** operator exports output fields to specified columns in a relational database table.

Input and Output
----------------

-  Input: fields to be exported
-  Output: relational database table

Parameters
----------

.. table:: **Table 1** Operator parameters description

   +------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                            | Node Type   | Mandatory   | Default Value |
   +==================+========================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | Output delimiter | Delimiter.                                                                                                                                                                                                                                                                                                                                                                                                                                             | string      | No          | ,             |
   |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                  | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                              |             |             |               |
   |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                  |    This configuration applies only to the MySQL dedicated connector. If the data column content contains the default delimiter, you need to set a user-defined delimiter. Otherwise, data disorder may occur.                                                                                                                                                                                                                                          |             |             |               |
   +------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Line delimiter   | Line delimiter, which can be any string specified by users based on the actual situation. Any character string is supported. The OS line delimiter is used by default.                                                                                                                                                                                                                                                                                 | string      | No          | ``\n``        |
   |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                  | .. note::                                                                                                                                                                                                                                                                                                                                                                                                                                              |             |             |               |
   |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                  |    This configuration applies only to the MySQL dedicated connector. If the data column content contains the default delimiter, you need to set a user-defined delimiter. Otherwise, data disorder may occur.                                                                                                                                                                                                                                          |             |             |               |
   +------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Output fields    | Information about relational database output fields:                                                                                                                                                                                                                                                                                                                                                                                                   | map         | Yes         | None          |
   |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                        |             |             |               |
   |                  | -  field name: Names of output fields.                                                                                                                                                                                                                                                                                                                                                                                                                 |             |             |               |
   |                  | -  table column name: Names of database table columns.                                                                                                                                                                                                                                                                                                                                                                                                 |             |             |               |
   |                  | -  type: Field type. The value must be consistent with the field type configured in the database.                                                                                                                                                                                                                                                                                                                                                      |             |             |               |
   |                  | -  length: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   +------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

The field values are exported to the table.

Example
-------

Use the data export from HBase to sqlserver2014 as an example.

In sqlserver2014, run the following statement to create an empty data test_1 for storing HBase data. Run the following statement:

**create table test_1 (id int, name text, value text);**

Use the HBase Input operator to generated three fields A, B, and C.

Use the **Table Output** operator to export A, B, and C to the test_1 table.

|image1|

The command output is as follows:

|image2|

.. |image1| image:: /_static/images/en-us_image_0000001296060012.png
.. |image2| image:: /_static/images/en-us_image_0000001348740037.jpg
