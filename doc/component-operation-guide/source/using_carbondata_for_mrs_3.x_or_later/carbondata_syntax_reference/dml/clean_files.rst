:original_name: mrs_01_1448.html

.. _mrs_01_1448:

CLEAN FILES
===========

Function
--------

After the **DELETE SEGMENT** command is executed, the deleted segments are marked as the **delete** state. After the segments are merged, the status of the original segments changes to **compacted**. The data files of these segments are not physically deleted. If you want to forcibly delete these files, run the **CLEAN FILES** command.

However, running this command may result in a query command execution failure.

Syntax
------

**CLEAN FILES FOR TABLE**\ * [db_name.]table_name* ;

Parameter Description
---------------------

.. table:: **Table 1** CLEAN FILES FOR TABLE parameters

   +------------+----------------------------------------------------------------------------------+
   | Parameter  | Description                                                                      |
   +============+==================================================================================+
   | db_name    | Database name. It consists of letters, digits, and underscores (_).              |
   +------------+----------------------------------------------------------------------------------+
   | table_name | Name of the database table. It consists of letters, digits, and underscores (_). |
   +------------+----------------------------------------------------------------------------------+

Precautions
-----------

None

Examples
--------

Add Carbon configuration parameters.

.. code-block::

   carbon.clean.file.force.allowed = true

**create table carbon01(a int,b string,c string) stored as carbondata;**

**insert into table carbon01 select 1,'a','aa';**

**insert into table carbon01 select 2,'b','bb';**

**delete from table carbon01 where segment.id in (0);**

**show segments for table carbon01;**

**CLEAN FILES FOR TABLE carbon01 options('force'='true');**

**show segments for table carbon01;**

In this example, all the segments marked as **deleted** and **compacted** are physically deleted.

System Response
---------------

Success or failure will be recorded in the driver logs.
