:original_name: mrs_01_1143.html

.. _mrs_01_1143:

Filter Rows
===========

Overview
--------

This **Filter Rows** operator filters rows that contain triggering conditions by configuring logic conditions.

Input and Output
----------------

-  Input: fields used to create filter conditions
-  Output: none

Parameter Description
---------------------

.. table:: **Table 1** Operator parameters description

   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter                 | Description                                                                                                                                  | Type        | Mandatory   | Default Value |
   +===========================+==============================================================================================================================================+=============+=============+===============+
   | Condition logic connector | Condition logic connector. The options include **AND** and **OR**.                                                                           | enum        | Yes         | AND           |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Conditions                | Filter condition information:                                                                                                                | map         | Yes         | None          |
   |                           |                                                                                                                                              |             |             |               |
   |                           | -  **input field name**: Names of the input fields. Set this parameter to the names of the fields generated in the previous conversion step. |             |             |               |
   |                           | -  **operator**: Operator                                                                                                                    |             |             |               |
   |                           | -  **comparative value**. You can directly enter the value of a field referenced in the **#{Existing field name}** format.                   |             |             |               |
   +---------------------------+----------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  When the condition logic is **AND**, if no filtering condition is added, all data becomes dirty data; if the original data meets all the added filtering conditions, the current line becomes dirty data.
-  When the condition logic is **OR**, if no filter condition is added, all data becomes dirty data; if the original data meets any of the added filter conditions, the current line becomes dirty data.

Example
-------

Use the **CSV File Input** operator to generate two fields A and B.

The following figure shows the source file.

|image1|

Configure the **Filter Rows** operator to filter lines that contain test.

|image2|

After the conversion, enter the original fields. The result is as follows:

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001295900064.jpg
.. |image2| image:: /_static/images/en-us_image_0000001296059904.png
.. |image3| image:: /_static/images/en-us_image_0000001349059749.jpg
