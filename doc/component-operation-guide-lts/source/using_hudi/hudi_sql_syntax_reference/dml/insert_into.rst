:original_name: mrs_01_24273.html

.. _mrs_01_24273:

INSERT INTO
===========

Function
--------

This command is used to insert the output of the **SELECT** statement to a Hudi table.

Syntax
------

**INSERT INTO** *tableIndentifier select query;*

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   ================ =======================
   Parameter        Description
   ================ =======================
   tableIndentifier Name of the Hudi table.
   select query     SELECT statement.
   ================ =======================

Precautions
-----------

-  Insert mode: Hudi supports three insert modes for tables with primary keys. You can set a parameter to specify the insert mode. The default value is **upsert**.

   #. In strict mode, the INSERT statement retains the primary key constraint of COW tables and is not allowed to insert duplicate records. If a record already exists during data insertion, HoodieDuplicateKeyException is thrown for COW tables. For MOR tables, the behavior in this mode is the same as that in upsert mode.
   #. In non-strict mode, records are inserted to primary key tables.
   #. In upsert mode, duplicate values in the primary key table are updated.

-  You can set **hoodie.sql.bulk.insert.enable** to **true** to enable the bulk insert statement as the write mode of the insert statement. Bulkinsert cannot be performed on the primary key table.

Examples
--------

.. code-block::

   insert into h0 select 1, 'a1', 20;

   -- insert static partition
   insert into h_p0 partition(dt = '2021-01-02') select 1, 'a1';

   -- insert dynamic partition
   insert into h_p0 select 1, 'a1', dt;

   -- insert dynamic partition
   insert into h_p1 select 1 as id, 'a1', '2021-01-03' as dt, '19' as hh;

   -- insert overwrite table
   insert overwrite table h0 select 1, 'a1', 20;

   -- insert overwrite table with static partition
   insert overwrite h_p0 partition(dt = '2021-01-02') select 1, 'a1';

   -- insert overwrite table with dynamic partition
   insert overwrite table h_p1 select 2 as id, 'a2', '2021-01-03' as dt, '19' as hh;

System Response
---------------

You can view the result in driver logs.
