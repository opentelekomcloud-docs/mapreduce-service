:original_name: mrs_01_24740.html

.. _mrs_01_24740:

CHANGE_TABLE
============

Function
--------

The **CHANGE_TABLE** command can be used to modify the type and index of a table. Key parameters such as the type and index of Hudi tables cannot be modified. Therefore, this command is actually used to rewrite Hudi tables.

Syntax
------

.. code-block::

   call change_table(table => '[table_name]', hoodie.index.type => '[index_type]', hoodie.datasource.write.table.type => '[table_type]');

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   ========== ================================
   Parameter  Description
   ========== ================================
   table_name Name of the table to be modified
   table_type Type of the table to be modified
   index_type Type of the index to be modified
   ========== ================================

Precautions
-----------

If the index type to be modified has other configuration parameters, the parameters must be transferred to the SQL statement in the **key =>'value'** format.

For example, to change the index type to bucket, run the following command:

.. code-block::

   call change_table(table => 'hudi_table1', hoodie.index.type => 'BUCKET', hoodie.bucket.index.num.buckets => '3');

Example
-------

call change_table(table => 'hudi_table1', hoodie.index.type => 'SIMPLE', hoodie.datasource.write.table.type => 'MERGE_ON_READ');

System Response
---------------

After the execution is complete, you can run the **desc formatted table** command to view the table properties.
