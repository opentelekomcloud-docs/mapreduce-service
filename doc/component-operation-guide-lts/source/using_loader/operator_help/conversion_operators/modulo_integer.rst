:original_name: mrs_01_1137.html

.. _mrs_01_1137:

Modulo Integer
==============

Overview
--------

The **Modulo Integer** operator performs modulo operations on integer fields to generate new fields.

Input and Output
----------------

-  Input: integer fields
-  Output: new fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameter description

   +---------------+--------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter     | Description                                                                                                                          | Type        | Mandatory   | Default Value |
   +===============+======================================================================================================================================+=============+=============+===============+
   | Modulo fields | Modulo operation information:                                                                                                        | map         | Yes         | None          |
   |               |                                                                                                                                      |             |             |               |
   |               | -  **input field name**: Names of input fields. Set this parameter to the names of fields generated in the previous conversion step. |             |             |               |
   |               | -  **output field name**: Names of output fields.                                                                                    |             |             |               |
   |               | -  **modulus**: Values used for a modulo operation.                                                                                  |             |             |               |
   +---------------+--------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  The operator generates new fields and the values are those after the modulo operation.
-  The field values must be integers; otherwise, the current line becomes dirty data.

Example
-------

Use the **CSV File Input** operator to generate fields A and B.

The following figure shows the source file.

|image1|

Configure the **Modulo Integer** operator to generate two new fields C and D.

|image2|

After the modulo operation, fields A, B, C, and D are generated, as shown in the following figure.

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001349259209.jpg
.. |image2| image:: /_static/images/en-us_image_0000001295900068.png
.. |image3| image:: /_static/images/en-us_image_0000001349059753.jpg
