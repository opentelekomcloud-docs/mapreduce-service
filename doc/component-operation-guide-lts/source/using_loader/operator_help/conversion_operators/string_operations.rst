:original_name: mrs_01_1140.html

.. _mrs_01_1140:

String Operations
=================

Overview
--------

The **String Operations** operator converts the upper and lower cases of existing fields to generate new fields.

Input and Output
----------------

-  Input: fields whose case is to be converted
-  Output: new fields after conversion

Parameter Description
---------------------

.. table:: **Table 1** Operator parameter description

   +------------------------+--------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter              | Description                                                                                                                          | Type        | Mandatory   | Default Value |
   +========================+======================================================================================================================================+=============+=============+===============+
   | Fields to be processed | Information about fields for string case conversion:                                                                                 | map         | Yes         | None          |
   |                        |                                                                                                                                      |             |             |               |
   |                        | -  **input field name**: Names of input fields. Set this parameter to the names of fields generated in the previous conversion step. |             |             |               |
   |                        | -  **output field name**: Names of output fields.                                                                                    |             |             |               |
   |                        | -  **lower/upper**: Indicates whether data is to be converted into uppercase letters or lowercase letters.                           |             |             |               |
   +------------------------+--------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  Case conversion is performed for strings.
-  If the input data is null, no case conversion is performed.

Example
-------

Use the **CSV File Input** operator to generate fields A and B.

The following figure shows the source file.

.. code-block::

   abcd,product
   FusionInsight,Bigdata

After configuring the **String Operations** operator, fields C and D are generated.

|image1|

After conversion, four fields are generated, as shown in the following figure.

.. code-block::

   abcd,product,ABCD,product
   FusionInsight,Bigdata,FUSIONINSIGHT,bigdata

.. |image1| image:: /_static/images/en-us_image_0000001348739897.png
