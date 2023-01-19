:original_name: mrs_01_1133.html

.. _mrs_01_1133:

Constant Field Addition
=======================

Overview
--------

The **Add Constants** operator generates constant fields.

Input and Output
----------------

-  Input: none
-  Output: constant fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameters description

   +-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                | Type        | Mandatory   | Default Value |
   +=================+============================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | Constant fields | Information about constant fields:                                                                                                                                                                                                                                                                                                                                                                                                                         | map         | Yes         | None          |
   |                 |                                                                                                                                                                                                                                                                                                                                                                                                                                                            |             |             |               |
   |                 | -  **output field name**: Names of the configured fields.                                                                                                                                                                                                                                                                                                                                                                                                  |             |             |               |
   |                 | -  **type**: field type                                                                                                                                                                                                                                                                                                                                                                                                                                    |             |             |               |
   |                 | -  **date format**: If the field type is **DATE**, **TIME**, or **TIMESTAMP**, you need to specify the time format. If the field type is neither of them, the time format is invalid. The example time format is **yyyyMMdd HH:mm:ss**.                                                                                                                                                                                                                    |             |             |               |
   |                 | -  **length**: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   |                 | -  **constant value**: Constant value of the correct type.                                                                                                                                                                                                                                                                                                                                                                                                 |             |             |               |
   +-----------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

This operator generates constant fields of the specified type.

Example
-------

Use the **CSV File Input** operator to generate two fields A and B.

The following figure shows the source file.

|image1|

Configure the **Add Constants** operator to add fields C and D.

|image2|

After adding the constants, fields A, B, C, and D are generated, as shown in the following figure.

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001349259117.jpg
.. |image2| image:: /_static/images/en-us_image_0000001348739841.png
.. |image3| image:: /_static/images/en-us_image_0000001295899980.jpg
