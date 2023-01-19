:original_name: mrs_01_1134.html

.. _mrs_01_1134:

Random Value Conversion
=======================

Overview
--------

**Generate Random** operator configures new values as random value fields.

Input and Output
----------------

-  Input: none
-  Output: random value fields

Parameter Description
---------------------

.. table:: **Table 1** Operator parameters description

   +-------------------+-----------------------------------------------------------------------+--------+-----------+---------------+
   | Parameter         | Description                                                           | Type   | Mandatory | Default Value |
   +===================+=======================================================================+========+===========+===============+
   | output field name | Names of generated random value fields.                               | string | Yes       | None          |
   +-------------------+-----------------------------------------------------------------------+--------+-----------+---------------+
   | length            | Field length.                                                         | map    | Yes       | None          |
   +-------------------+-----------------------------------------------------------------------+--------+-----------+---------------+
   | type              | Field type. The options are **VARCHAR**, **INTEGER**, and **BIGINT**. | enum   | Yes       | VARCHAR       |
   +-------------------+-----------------------------------------------------------------------+--------+-----------+---------------+

Data Processing Rule
--------------------

The operator generates random value fields of specified type.

Example
-------

Use the **CSV File Input** operator to generate two fields A and B.

The following figure shows the source file.

|image1|

Configure the random value conversion operator to generate fields C, D, and E.

|image2|

Five fields are generated.

|image3|

The random value fields generated each time are different.

.. |image1| image:: /_static/images/en-us_image_0000001348740169.png
.. |image2| image:: /_static/images/en-us_image_0000001296060140.png
.. |image3| image:: /_static/images/en-us_image_0000001296219768.jpg
