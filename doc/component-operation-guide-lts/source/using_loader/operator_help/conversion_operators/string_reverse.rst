:original_name: mrs_01_1141.html

.. _mrs_01_1141:

String Reverse
==============

Overview
--------

The **String Reverse** operator reverses existing fields to generate new fields.

Input and Output
----------------

-  Input: fields to be reversed
-  Output: new fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameter description

   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                          | Type        | Mandatory   | Default Value |
   +=======================+======================================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | Fields to be reversed | Information about fields for string reversal conversion:                                                                                                                                                                                                                                                                                                                                                                                                             | map         | Yes         | None          |
   |                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |             |             |               |
   |                       | -  **input field name**: Names of input fields. Set this parameter to the names of fields generated in the previous conversion step.                                                                                                                                                                                                                                                                                                                                 |             |             |               |
   |                       | -  **output field name**: Names of output fields.                                                                                                                                                                                                                                                                                                                                                                                                                    |             |             |               |
   |                       | -  **type**: Field type.                                                                                                                                                                                                                                                                                                                                                                                                                                             |             |             |               |
   |                       | -  **out field length**: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   +-----------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  Value reversal conversion is performed for fields.
-  If the input data is null, no reversal conversion is performed.
-  If the number of input field columns is greater than the number of field columns actually included in the original data, all data becomes dirty data.

Example
-------

Use the **CSV File Input** operator to generate fields A and B.

The following figure shows the source file.

.. code-block::

   abcd,product
   FusionInsight,Bigdata

Configure the **String Reverse** operator to generate two new fields C and D.

|image1|

After conversion, four fields are generated, as shown in the following figure.

.. code-block::

   abcd,product,dcba,tcudorp
   FusionInsight,Bigdata,thgisnInoisuF,atadgiB

.. |image1| image:: /_static/images/en-us_image_0000001349259393.png
