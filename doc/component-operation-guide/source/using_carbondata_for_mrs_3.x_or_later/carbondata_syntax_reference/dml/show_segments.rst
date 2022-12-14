:original_name: mrs_01_1444.html

.. _mrs_01_1444:

SHOW SEGMENTS
=============

Function
--------

This command is used to list the segments of a CarbonData table.

Syntax
------

**SHOW SEGMENTS FOR TABLE** *[db_name.]table_name* **LIMIT** *number_of_loads;*

Parameter Description
---------------------

.. table:: **Table 1** SHOW SEGMENTS FOR TABLE parameters

   +-----------------+----------------------------------------------------------------------------------+
   | Parameter       | Description                                                                      |
   +=================+==================================================================================+
   | db_name         | Database name. If this parameter is not specified, the current database is used. |
   +-----------------+----------------------------------------------------------------------------------+
   | table_name      | Name of a table in the specified database                                        |
   +-----------------+----------------------------------------------------------------------------------+
   | number_of_loads | Threshold of records to be listed                                                |
   +-----------------+----------------------------------------------------------------------------------+

Precautions
-----------

None

Examples
--------

**create table** **carbon01(a int,b string,c string) stored as carbondata;**

**insert into** **table** **carbon01 select 1,'a','aa';**

**insert into table** **carbon01 select 2,'b','bb';**

**insert into table** **carbon01 select 3,'c','cc';**

**SHOW SEGMENTS FOR TABLE** **carbon01** **LIMIT** **2;**

System Response
---------------

.. code-block::

   +-----+----------+--------------------------+------------------+------------+------------+-------------+--------------+--+
   | ID  |  Status  |     Load Start Time      | Load Time Taken  | Partition  | Data Size  | Index Size  | File Format  |
   +-----+----------+--------------------------+------------------+------------+------------+-------------+--------------+--+
   | 3   | Success  | 2020-09-28 22:53:26.336  | 3.726S           | {}         | 6.47KB     | 3.30KB      | columnar_v3  |
   | 2   | Success  | 2020-09-28 22:53:01.702  | 6.688S           | {}         | 6.47KB     | 3.30KB      | columnar_v3  |
   +-----+----------+--------------------------+------------------+------------+------------+-------------+--------------+--+
