:original_name: mrs_01_1142.html

.. _mrs_01_1142:

String Trim
===========

Overview
--------

The **String Trim** operator clears spaces contained in existing fields to generate new fields.

Input and Output
----------------

-  Input: fields whose spaces are to be cleared
-  Output: new fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameter description

   +----------------------+--------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter            | Description                                                                                                                          | Type        | Mandatory   | Default Value |
   +======================+======================================================================================================================================+=============+=============+===============+
   | Fields to be trimmed | Information about fields for clearing spaces contained in strings:                                                                   | map         | Yes         | None          |
   |                      |                                                                                                                                      |             |             |               |
   |                      | -  **input field name**: Names of input fields. Set this parameter to the names of fields generated in the previous conversion step. |             |             |               |
   |                      | -  **output field name**: Names of output fields.                                                                                    |             |             |               |
   |                      | -  **trim type**: Space clearing mode (clearing starting spaces, ending spaces, or starting and ending spaces).                      |             |             |               |
   +----------------------+--------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  Clearing spaces at both ends of a value supports clearing spaces at the left end, at the right end, and at both ends.
-  If the input data is null, no conversion is performed.
-  If the number of input field columns is greater than the number of field columns actually included in the original data, all data becomes dirty data.

Example
-------

Use the **CSV File Input** operator to generate fields A, B, and C.

The following figure shows the source file.

|image1|

Configure the **String Trim** operator to generate three new fields D, E, and F.

|image2|

Six fields are generated, as shown in the following figure.

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001296219724.jpg
.. |image2| image:: /_static/images/en-us_image_0000001295740292.png
.. |image3| image:: /_static/images/en-us_image_0000001349139809.jpg
