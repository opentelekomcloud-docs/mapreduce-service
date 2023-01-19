:original_name: mrs_01_1149.html

.. _mrs_01_1149:

File Output
===========

Overview
--------

The **File Output** operator uses delimiters to concatenate existing fields and exports new fields to a file.

Input and Output
----------------

-  Input: fields to be exported
-  Output: files

Parameter Description
---------------------

.. table:: **Table 1** Operator parameters description

   +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Parameter        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                | Type        | Mandatory   | Default Value |
   +==================+============================================================================================================================================================================================================================================================================================================================================================================================================================================================+=============+=============+===============+
   | Output delimiter | Set a delimiter.                                                                                                                                                                                                                                                                                                                                                                                                                                           | string      | Yes         | None          |
   +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Line breaker     | Line delimiter, which can be any string specified by users based on the actual situation. Any character string is supported. The OS line delimiter is used by default.                                                                                                                                                                                                                                                                                     | string      | No          | ``\n``        |
   +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+
   | Output fields    | Information about output fields:                                                                                                                                                                                                                                                                                                                                                                                                                           | map         | No          | None          |
   |                  |                                                                                                                                                                                                                                                                                                                                                                                                                                                            |             |             |               |
   |                  | -  **position**: Position of output fields.                                                                                                                                                                                                                                                                                                                                                                                                                |             |             |               |
   |                  | -  **field name**: Names of output fields.                                                                                                                                                                                                                                                                                                                                                                                                                 |             |             |               |
   |                  | -  **type**: Field type. If type is set to **DATE**, **TIME**, or **TIMESTAMP**, you must specify a time format. If type is set to other values, the time format is invalid. The example time format is **yyyyMMdd HH:mm:ss**.                                                                                                                                                                                                                             |             |             |               |
   |                  | -  **length**: Field value length. If the actual field value is excessively long, the value is cut based on the configured length. When **type** is set to **CHAR**, spaces are added to the field value for supplement if the actual field value length is less than the configured length. When **type** is set to **VARCHAR**, no space is added to the field value for supplement if the actual field value length is less than the configured length. |             |             |               |
   +------------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------+-------------+---------------+

Data Processing Rule
--------------------

The field is exported to a file.

Example
-------

Use the **CSV File Input** operator to generate two fields A and B.

The following figure shows the source file.

.. code-block::

   aaa,product
   bbb,Bigdata

Configure the **File Output** operator, set **Output delimiter** to a comma (,), and export A and B to a file, as shown in the following figure.

|image1|

The following figure shows the result.

.. code-block::

   aaa,product
   bbb,Bigdata

.. |image1| image:: /_static/images/en-us_image_0000001349139685.png
