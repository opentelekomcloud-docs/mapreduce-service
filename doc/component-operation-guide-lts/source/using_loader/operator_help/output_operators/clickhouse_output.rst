:original_name: mrs_01_24177.html

.. _mrs_01_24177:

ClickHouse Output
=================

Overview
--------

The **ClickHouse Output** operator exports existing fields to specified columns of a ClickHouse table.

Input and Output
----------------

-  Input: fields to be exported
-  Output: ClickHouse table

Parameters
----------

.. table:: **Table 1** Operator parameters

   +--------------------------+--------------------------------------------------------+--------+-----------+---------------+
   | Parameter                | Description                                            | Type   | Mandatory | Default Value |
   +==========================+========================================================+========+===========+===============+
   | ClickHouse database name | Database where the ClickHouse table is located.        | string | Yes       | default       |
   +--------------------------+--------------------------------------------------------+--------+-----------+---------------+
   | ClickHouse table name    | Name of the ClickHouse table to which data is written. | string | Yes       | None          |
   +--------------------------+--------------------------------------------------------+--------+-----------+---------------+

Data Processing Rule
--------------------

The field values are exported to the ClickHouse table.

Example
-------

Use the **CSV File Input** operator to generate 12 fields.

The following figure shows the source file.

|image1|

Run the following statements to create a ClickHouse table:

**CREATE TABLE IF NOT EXISTS testck4 ON CLUSTER default_cluster(**

**a Int32,**

**b VARCHAR(100) NOT NULL,**

**c char(100),**

**d DateTime,**

**e DateTime,**

**f DateTime,**

**g smallint,**

**h bigint,**

**l Float32,**

**j Float64,**

**k decimal(10,2),**

**m boolean**

**)**

**ENGINE = ReplicatedMergeTree('/clickhouse/tables/{shard}/default/testck4', '{replica}')**

**PARTITION BY toYYYYMM(d)ORDER BY a;**

Configure the **ClickHouse Output** operator, as shown in the following figure.

|image2|

After the job execution is complete, view the data in the **testck4** table.

|image3|

.. |image1| image:: /_static/images/en-us_image_0000001349059881.png
.. |image2| image:: /_static/images/en-us_image_0000001349259329.png
.. |image3| image:: /_static/images/en-us_image_0000001349139745.png
