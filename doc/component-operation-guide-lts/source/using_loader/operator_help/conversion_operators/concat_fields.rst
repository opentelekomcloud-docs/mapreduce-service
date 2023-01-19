:original_name: mrs_01_1135.html

.. _mrs_01_1135:

Concat Fields
=============

Overview
--------

The **Concat Fields** operator concatenates existing fields by using delimiters to generate new fields.

Input and Output
----------------

-  Input: fields to be concatenated
-  Output: new fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameter description

   +---------------------+---------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter           | Description                                                                                                                     | Type        | Mandatory   | Default Value |
   +=====================+=================================================================================================================================+=============+=============+===============+
   | Output field name   | Name of a field generated after concatenation.                                                                                  | string      | Yes         | None          |
   +---------------------+---------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Delimiter           | Concatenation character. The value can be blank.                                                                                | string      | No          | Empty string  |
   +---------------------+---------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Fields to be merged | Names of fields to be concatenated.                                                                                             | map         | Yes         | None          |
   |                     |                                                                                                                                 |             |             |               |
   |                     | **field name** must be set to the names of fields generated in the previous conversion step. Multiple field names can be added. |             |             |               |
   +---------------------+---------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  Use delimiters to concatenate the fields specified by **Fields to be merged** in order and assign the output to **Output field name**.
-  If the value of a field is null, the value is changed to an empty string and then concatenated with other field values.

Example
-------

Use the **CSV File Input** operator to generate fields A, B, and C.

The following figure shows the source file.

|image1|

Configure the **Concat Fields** operator, set **Delimiter** to blank space, and generate field D.

|image2|

After concatenation, fields A, B, C, and D are generated, as shown in the following figure.

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001348740001.jpg
.. |image2| image:: /_static/images/en-us_image_0000001349139689.png
.. |image3| image:: /_static/images/en-us_image_0000001349259277.jpg
