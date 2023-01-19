:original_name: mrs_01_1131.html

.. _mrs_01_1131:

Long Date Conversion
====================

Overview
--------

The **Long Date Conversion** operator performs long integer and date conversion.

Input and Output
----------------

-  Input: fields to be converted
-  Output: new fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameter description

   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter         | Description                                                                                                                                                  | Type        | Mandatory   | Default Value |
   +===================+==============================================================================================================================================================+=============+=============+===============+
   | convert type      | Types of long integer and date conversion:                                                                                                                   | enum        | Yes         | long to date  |
   |                   |                                                                                                                                                              |             |             |               |
   |                   | -  **long to date**: converts long integers to date.                                                                                                         |             |             |               |
   |                   | -  **long to time**: converts long integers to time.                                                                                                         |             |             |               |
   |                   | -  **long to timestamp**: converts long integers to timestamp.                                                                                               |             |             |               |
   |                   | -  **date to long**: converts date to long integers.                                                                                                         |             |             |               |
   |                   | -  **time to long**: converts time to long integers.                                                                                                         |             |             |               |
   |                   | -  **timestamp to long**: converts timestamp to long integers.                                                                                               |             |             |               |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | input field name  | Name of input fields to be converted. Set this parameter to the names of fields generated in the previous conversion step.                                   | string      | Yes         | None          |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | output field name | Names of output fields.                                                                                                                                      | string      | Yes         | None          |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | field unit        | Unit of a long integer field. According to **convert type**, the value is an input field or generated field. The options are **second** and **millisecond**. | enum        | Yes         | second        |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | output field type | Output field type. The options are **BIGINT**, **DATE**, **TIME**, and **TIMESTAMP**.                                                                        | enum        | Yes         | BIGINT        |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | date format       | Time field format, for example, **yyyyMMdd HH:mm:ss**.                                                                                                       | string      | No          | None          |
   +-------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  If the original data includes null values, no conversion is performed.
-  If the number of input field columns is greater than the number of field columns actually included in the original data, all data becomes dirty data.
-  If a type conversion error occurs, the current data is saved as dirty data.

Example
-------

Use the **CSV File Input** operator to generate fields A and B.

The following figure shows the source file.

|image1|

Configure the **Long Date Conversion** operator to generate four new fields C, D, E, and F. Their types are DATE, TIME, TIMESTAMP, and BIGINT, respectively.

|image2|

The following figure shows the output of the conversion.

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001349259249.jpg
.. |image2| image:: /_static/images/en-us_image_0000001349139657.png
.. |image3| image:: /_static/images/en-us_image_0000001295900108.jpg
