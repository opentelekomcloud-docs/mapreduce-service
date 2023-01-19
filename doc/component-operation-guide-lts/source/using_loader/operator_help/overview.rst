:original_name: mrs_01_1120.html

.. _mrs_01_1120:

Overview
========

Conversion Process
------------------

Loader reads data at the source end, uses an input operator to convert data into fields by certain rules, use a conversion operator to clean or convert the fields, and finally use an output operator to process the fields and export the output result to the target end.

-  A job for performing data conversion can have only one input operator and one output operator.
-  Data that does not meet conversion rules will become dirty data and be skipped.

.. note::

   -  For the data import from a relational database to HDFS/OBS, data conversion does not need to be configured and the data is separated using commas (**,**) and saved to HDFS/OBS.
   -  For the data import from HDFS/OBS to a relational database, data conversion does not need to be configured and the data is separated using commas (**,**) and saved to the relational database.

Operator Description
--------------------

Loader operators have three types:

-  Input Operators

   First step of data conversion. This type of operator converts data into fields. Only one input operator can be used in each conversion. The input operator is mandatory in HBase or Hive data import and export.

-  Conversion Operators

   Intermediate conversion step of data conversion. This type of operator is optional. The conversion operators can be used together in any combination. Conversion operators can process only fields. Therefore, an input operator must be used first to convert data into fields.

-  Output Operators

   Last step of data conversion. Only one output operator can be used in each conversion for exporting processed fields. The output operator is mandatory in HBase or Hive data import and export.

   .. table:: **Table 1** List of operator types

      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Node Type                         | Description                                                                                                                                                                |
      +===================================+============================================================================================================================================================================+
      | Input:                            | -  CSV file input: Each line in the file is converted into multiple input fields based on the specified delimiter.                                                         |
      |                                   | -  Fixed-width file input: Each line of the file is converted into multiple input fields based on the characters or bytes with configurable length.                        |
      |                                   | -  Table input: converts specified columns in a relational database table into input fields of the same quantity.                                                          |
      |                                   | -  HBase input: converts specified columns in an HBase table into input fields of the same quantity.                                                                       |
      |                                   | -  HTML input: converts elements in an HTML file into input fields.                                                                                                        |
      |                                   | -  Hive input: converts specified columns in a Hive table into input fields of the same quantity.                                                                          |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Convert                           | -  Long integer to time conversion: Implements the conversion between long integer values and date types.                                                                  |
      |                                   | -  Null value conversion: Replaces a null value with a specified value.                                                                                                    |
      |                                   | -  Constant field adding: Generates a constant field.                                                                                                                      |
      |                                   | -  Random value conversion: generates a random number field.                                                                                                               |
      |                                   | -  Concatenation and conversion: concatenates existing fields to generate new fields.                                                                                      |
      |                                   | -  Delimiter conversion: separates existing fields with specified separators to generate new fields.                                                                       |
      |                                   | -  Modulo conversion: performs modulo operation on an existing field to generate a new field.                                                                              |
      |                                   | -  Charater string cutting: cuts existing string fields by the specified start position and end position to generate new fields.                                           |
      |                                   | -  EL operation conversion: specifies a calculator to calculate field values. Currently, the following operators are supported: md5sum, sha1sum, sha256sum, and sha512sum. |
      |                                   | -  Character string case conversion: converts the upper and lower cases of existing fields to generate new fields.                                                         |
      |                                   | -  Character string reverse conversion: reverses existing character string fields to generate new fields.                                                                  |
      |                                   | -  Character string space clearing and conversion: clears the spaces on the left and right of the existing character string fields to generate new fields.                 |
      |                                   | -  Row filtering conversion: filters rows that contain triggering conditions by configuring logic conditions.                                                              |
      |                                   | -  Domain update: updates fields values when certain conditions are met.                                                                                                   |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Output:                           | -  Hive Output: exports existing fields to a Hive table.                                                                                                                   |
      |                                   | -  Table output: exports existing fields to a relational database table.                                                                                                   |
      |                                   | -  File output: uses delimiters to concatenate existing fields and exports new fields to a file.                                                                           |
      |                                   | -  HBase Output: exports existing fields to an HBase table.                                                                                                                |
      +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Field Description
-----------------

Fields in the job configuration are data items defined by Loader based on service requirements to match user data. Fields have specific types and the fields types must be consistent with the actual user data types.
