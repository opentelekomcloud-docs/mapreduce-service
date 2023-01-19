:original_name: mrs_01_24277.html

.. _mrs_01_24277:

COMPACTION
==========

Function
--------

This command is used to convert row-based log files in MOR tables into column-based data files in parquet tables to accelerate record search.

Syntax
------

**SCHEDULE COMPACTION** on *tableIdentifier* \|tablelocation;

**SHOW COMPACTION** on *tableIdentifier* \|tablelocation;

**RUN COMPACTION** on *tableIdentifier* \|tablelocation [at instant-time];

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +-----------------+----------------------------------------------------------------------------------------------------------+
   | Parameter       | Description                                                                                              |
   +=================+==========================================================================================================+
   | tableIdentifier | Name of the Hudi table to convert log files.                                                             |
   +-----------------+----------------------------------------------------------------------------------------------------------+
   | tablelocation   | The storage path of the Hudi table.                                                                      |
   +-----------------+----------------------------------------------------------------------------------------------------------+
   | instant-time    | Time to run the command. You can run the **show compaction** command to view the **instant-time** value. |
   +-----------------+----------------------------------------------------------------------------------------------------------+

Examples
--------

.. code-block::

   schedule compaction  on h1;
   show compaction on h1;
   run compaction on h1 at 20210915170758;

   schedule compaction  on '/tmp/hudi/h1';
   run compaction on '/tmp/hudi/h1';

Precautions
-----------

You need to set **hoodie.payload.ordering.field** to the value of **preCombineField** when you use the Hudi CLI or API to trigger compaction for the Hudi table created by SQL.

System Response
---------------

You can view the result in driver logs or on the client.
