:original_name: mrs_01_1132.html

.. _mrs_01_1132:

Null Value Conversion
=====================

Overview
--------

The **null value conversion** operator replaces null values with specified values.

Input and Output
----------------

-  Input: fields with null values
-  Output: original fields with new values

Parameter Description
---------------------

.. table:: **Table 1** Operator parameters description

   +-----------------------+------------------------------------------------------------------------------------------------+-----------+-----------+---------------+
   | Parameter             | Description                                                                                    | Node Type | Mandatory | Default Value |
   +=======================+================================================================================================+===========+===========+===============+
   | Input field name      | Names of fields that may have null values. Set this parameter to the names of existing fields. | string    | Yes       | None          |
   +-----------------------+------------------------------------------------------------------------------------------------+-----------+-----------+---------------+
   | Replace by this value | Specified values for replacing null values.                                                    | string    | Yes       | None          |
   +-----------------------+------------------------------------------------------------------------------------------------+-----------+-----------+---------------+

Data Processing Rule
--------------------

When field values are empty, specified values are added.

Example
-------

Use the **CSV File Input** operator to generate two fields A and B.

The following figure shows the source file.

|image1|

Configure the **null value conversion** operator, as shown in the following figure.

|image2|

After replacement, the values of fields A and B are as follows:

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001348739825.jpg
.. |image2| image:: /_static/images/en-us_image_0000001349139513.png
.. |image3| image:: /_static/images/en-us_image_0000001296219432.jpg
