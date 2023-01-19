:original_name: mrs_01_1122.html

.. _mrs_01_1122:

CSV File Input
==============

Overview
--------

The **CSV File Input** operator imports all files that can be opened by using a text editor.

Input and Output
----------------

-  Input: test files
-  Output: fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameter description

   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                | Type        | Mandatory   | Default Value |
   +======================+============================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | Delimiter            | Delimiter in a CSV file for separating data lines.                                                                                                                                                                                                                                                                                                                                                                                                         | string      | Yes         | ,             |
   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Line Delimiter       | Line delimiter, which can be any string specified by users based on the actual situation. The OS line delimiter is used by default.                                                                                                                                                                                                                                                                                                                        | string      | No          | ``\n``        |
   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Filename as field    | User-defined field whose value is the name of the file that stores the current data.                                                                                                                                                                                                                                                                                                                                                                       | string      | No          | None          |
   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Absolute path        | Indicates whether the file name used as the value of **Filename as field** contains an absolute path. Selecting the option button indicates that the file name contains an absolute path; deselecting the option button indicates that the file name does not contain a path.                                                                                                                                                                              | boolean     | No          | Deselect      |
   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Validate input field | Checks whether the input field matches the value type. If the value is **NO**, no check is performed. If the value is **YES**, whether the input field matches the value type is checked. If the input fields do not match the value type, the line is skipped.                                                                                                                                                                                            | enum        | Yes         | YES           |
   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Input fields         | Information about input fields:                                                                                                                                                                                                                                                                                                                                                                                                                            | map         | Yes         | None          |
   |                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                            |             |             |               |
   |                      | -  **position**: Position of the field after data lines in the source file are separated by delimiters. The position sequence starts from 1.                                                                                                                                                                                                                                                                                                               |             |             |               |
   |                      | -  **field name**: Field name.                                                                                                                                                                                                                                                                                                                                                                                                                             |             |             |               |
   |                      | -  **type**: Field type.                                                                                                                                                                                                                                                                                                                                                                                                                                   |             |             |               |
   |                      | -  **date format**: If the field type is **DATE**, **TIME**, or **TIMESTAMP**, you must specify a time format. If the field type is set to other values, the time format is invalid. An example time format is **yyyyMMdd HH:mm:ss**.                                                                                                                                                                                                                      |             |             |               |
   |                      | -  **length**: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  Each data line is separated into multiple fields by using delimiters and the fields are used by the subsequent conversion operator.
-  If the field value does not match the actual type, the data in the line will become dirty data.
-  If the number of input field columns is equal to the number of field columns actually included in the original data, the data in the line will become dirty data.

Example
-------

The following figure shows the source file.

|image1|

Configure the **CSV File Input** operator, set **Delimiter** to a comma (**,**), and generate fields A and B.

|image2|

Fields A and B are generated, as shown in the following figure.

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001295740268.jpg
.. |image2| image:: /_static/images/en-us_image_0000001349139781.jpg
.. |image3| image:: /_static/images/en-us_image_0000001295900228.jpg
