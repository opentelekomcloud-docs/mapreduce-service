:original_name: mrs_01_1126.html

.. _mrs_01_1126:

HTML Input
==========

Overview
--------

**HTML Input** operator imports a regular HTML file and converts elements in the HTML file into input fields.

Input and Output
----------------

Input: HTML file

Output: multiple fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameters description

   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                | Type        | Mandatory   | Default Value |
   +======================+============================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | parent tag           | Upper-layer HTML tag of all fields for limiting the search scope.                                                                                                                                                                                                                                                                                                                                                                                          | string      | Yes         | None          |
   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Filename as field    | User-defined field whose value is the name of the file that stores the current data.                                                                                                                                                                                                                                                                                                                                                                       | string      | No          | None          |
   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Absolute file name   | Whether the file name used as the value of **Filename as field** contains an absolute path. Selecting the option button indicates that the file name contains an absolute path; deselecting the option button indicates that the file name does not contain a path.                                                                                                                                                                                        | boolean     | No          | No            |
   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Validate input field | Whether to check the type matching between the input field and the value. If the value is **NO**, the field is not checked. If the value is **YES**, the field will be checked. If the input field does not match the value type, the line is skipped.                                                                                                                                                                                                     | enum        | Yes         | YES           |
   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Input fields         | Information about input fields:                                                                                                                                                                                                                                                                                                                                                                                                                            | map         | Yes         | None          |
   |                      |                                                                                                                                                                                                                                                                                                                                                                                                                                                            |             |             |               |
   |                      | -  **position**: Position of the field. The position sequence starts from 1.                                                                                                                                                                                                                                                                                                                                                                               |             |             |               |
   |                      | -  **field name**: field name                                                                                                                                                                                                                                                                                                                                                                                                                              |             |             |               |
   |                      | -  **field tag**: field tag                                                                                                                                                                                                                                                                                                                                                                                                                                |             |             |               |
   |                      | -  **keyword**: A keyword can be configured to match the content of the tag. Wildcards are supported. For example, if the tag content is **name**, you can configure the keyword **\*name\***.                                                                                                                                                                                                                                                             |             |             |               |
   |                      | -  **type**: field type                                                                                                                                                                                                                                                                                                                                                                                                                                    |             |             |               |
   |                      | -  **date format**: If the field type is **DATE**, **TIME**, or **TIMESTAMP**, you need to specify the time format. If the field type is neither of them, the time format is invalid. The example time format is **yyyyMMdd HH:mm:ss**.                                                                                                                                                                                                                    |             |             |               |
   |                      | -  **length**: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   +----------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

-  **parent tag** is configured first to limit the search scope. The value of **parent tag** must exist; otherwise, the obtained content is empty.
-  **Input fields** are configured so that the sub-tags can be used to precisely locate the tags of fields. If the tags are the same, keywords will be used for precise matching.
-  The keyword is used to match the content of the field. The configuration method is similar to that of the **File filter** field in the **From** settings. The wildcard **(*)** is supported. The following three tags are provided to assist in locating the field:

   #. **#PART**: indicates the values matched by wildcard **\***. If there are multiple **\***, you can specify an order from left to right and obtain content that matches the sequence number **\***. For example, **#PART1** indicates to obtain the value that matches the first **\*** and **#PART8** indicates to obtain the value that matches the eighth **\***).
   #. **#NEXT**: indicates that you can obtain the value next to the value that matches the tag.
   #. **#ALL**: indicates that you can obtain all the values that match the tag.

-  If the tag is configured incorrectly, the obtained value is empty, but no error is reported.

Example
-------

The following figure shows the source file.

|image1|

Configure the **HTML Input** operator to generate fields A, B, and C.

|image2|

Three fields are generated, as shown in the following figure.

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001296219464.jpg
.. |image2| image:: /_static/images/en-us_image_0000001296059832.png
.. |image3| image:: /_static/images/en-us_image_0000001349139545.jpg
