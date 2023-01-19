:original_name: mrs_01_1136.html

.. _mrs_01_1136:

Extract Fields
==============

Overview
--------

The **Extract Fields** separates an existing field by using delimiters to generate new fields.

Input and Output
----------------

-  Input: field to be separated
-  Output: new fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameter description

   +------------------+-----------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter        | Description                                                                                                           | Type        | Mandatory   | Default Value |
   +==================+=======================================================================================================================+=============+=============+===============+
   | Input field name | Name of a field to be separated. Set this parameter to the name of a field generated in the previous conversion step. | string      | Yes         | None          |
   +------------------+-----------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Delimiter        | Delimiter.                                                                                                            | string      | Yes         | None          |
   +------------------+-----------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Fields extracted | Fields generated after field separation. Multiple fields can be generated after field separation.                     | map         | Yes         | None          |
   |                  |                                                                                                                       |             |             |               |
   |                  | -  **position**: Position of fields generated after field separation.                                                 |             |             |               |
   |                  | -  **output field name**: Names of output fields.                                                                     |             |             |               |
   +------------------+-----------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  The value of the input field is separated by specified delimiters and the segments are assigned to the new fields.
-  If the number of field columns after separation is greater than the actual number allowed by the original data, the line will become dirty data.

Example
-------

Use the **CSV File Input** operator to generate field A.

The following figure shows the source file.

|image1|

Configure the **Extract Fields** operator, set **Delimiter** to blank space, and generate three fields B, C, and D.

|image2|

After conversion, fields A, B, C, and D are generated, as shown in the following figure.

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001349139673.jpg
.. |image2| image:: /_static/images/en-us_image_0000001349259265.png
.. |image3| image:: /_static/images/en-us_image_0000001348739989.jpg
