:original_name: mrs_01_1138.html

.. _mrs_01_1138:

String Cut
==========

Overview
--------

The **String Cut** operator cuts existing fields to generate new fields.

Input and Output
----------------

-  Input: fields to be cut
-  Output: new fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameter description

   +------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Type        | Mandatory   | Default Value |
   +==================+===================================================================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | Fields to be cut | Information about a cut field:                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | map         | Yes         | None          |
   |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |             |             |               |
   |                  | -  **input field name**: Names of input fields. Set this parameter to the names of fields generated in the previous conversion step.                                                                                                                                                                                                                                                                                                                                                              |             |             |               |
   |                  | -  **output field name**: Names of output fields.                                                                                                                                                                                                                                                                                                                                                                                                                                                 |             |             |               |
   |                  | -  **start position**: Cutting start position, starting from sequence 1.                                                                                                                                                                                                                                                                                                                                                                                                                          |             |             |               |
   |                  | -  **end position**: Cutting end position. If the length of the cut string cannot be determined, you can set this parameter to -1, indicating the end of a string to be cut.                                                                                                                                                                                                                                                                                                                      |             |             |               |
   |                  | -  **output field type**: Type of output fields.                                                                                                                                                                                                                                                                                                                                                                                                                                                  |             |             |               |
   |                  | -  **output field length**: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **output field type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **output field type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   +------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  **start position** and **end position** are used to cut the original fields and generate new fields.
-  If **end position** is set to **-1**, the end of a string is to be cut. In other cases, the value of **end position** must be greater than the value of **start position**.
-  If the value of **start position** or **end position** is greater than the length of the input field, the line will become dirty data.

Example
-------

Use the **CSV File Input** operator to generate fields A and B.

The following figure shows the source file.

.. code-block::

   abcd,product
   FusionInsight,Bigdata

After configuring the **String Cut** operator, fields C and D are generated.

|image1|

After cutting, the following fields are generated.

.. code-block::

   abcd,product,abc,prod
   FusionInsight,Bigdata,Fus,Bigd

.. |image1| image:: /_static/images/en-us_image_0000001295740272.png
