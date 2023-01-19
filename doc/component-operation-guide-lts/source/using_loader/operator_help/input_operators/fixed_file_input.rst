:original_name: mrs_01_1123.html

.. _mrs_01_1123:

Fixed File Input
================

Overview
--------

The **Fixed File Input** operator converts each line in a file into multiple fields by character or byte of a configurable length.

Input and Output
----------------

-  Input: text file
-  Output: fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameter description

   +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter         | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                | Type        | Mandatory   | Default Value |
   +===================+============================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | Line Delimiter    | Line delimiter, which can be any string specified by users based on the actual situation. The OS line delimiter is used by default.                                                                                                                                                                                                                                                                                                                        | string      | No          | ``\n``        |
   +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Fixed length unit | Length unit. The options are **char** and **byte**.                                                                                                                                                                                                                                                                                                                                                                                                        | enum        | Yes         | char          |
   +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Input fields      | Information about input fields:                                                                                                                                                                                                                                                                                                                                                                                                                            | map         | Yes         | None          |
   |                   |                                                                                                                                                                                                                                                                                                                                                                                                                                                            |             |             |               |
   |                   | -  **fixed length**: Field length. The ending of the first field is the starting of the second field, the ending of the second field is the starting of the third field, and so on.                                                                                                                                                                                                                                                                        |             |             |               |
   |                   | -  **field name**: Names of input fields.                                                                                                                                                                                                                                                                                                                                                                                                                  |             |             |               |
   |                   | -  **type**: Field type.                                                                                                                                                                                                                                                                                                                                                                                                                                   |             |             |               |
   |                   | -  **date format**: If the field type is **DATE**, **TIME**, or **TIMESTAMP**, you must specify a time format. If the field type is set to other values, the time format is invalid. An example time format is **yyyyMMdd HH:mm:ss**.                                                                                                                                                                                                                      |             |             |               |
   |                   | -  **length**: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   +-------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  The source file is split based on the input field length to generate fields.
-  If the field value does not match the actual type, the data in the line will become dirty data.
-  If the field split length is greater than the length of the original field value, the data split fails and the line becomes dirty data.

Example
-------

The following figure shows the source file.

|image1|

Configure the **Fixed File Input** operator to generate fields A, B, and C.

|image2|

The three fields are generated, as shown in the following figure.

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001295900008.jpg
.. |image2| image:: /_static/images/en-us_image_0000001348739869.png
.. |image3| image:: /_static/images/en-us_image_0000001295740040.jpg
