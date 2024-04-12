:original_name: mrs_01_24781.html

.. _mrs_01_24781:

CLEAN_FILE
==========

Function
--------

Cleans invalid data files from the Hudi table directory.

Syntax
------

**call clean_file**\ (table => '[table_name]', mode=>'[op_type]', backup_path=>'[backup_path]', start_instant_time=>'[start_time]', end_instant_time=>'[end_time]');

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Parameter                         | Description                                                                                                                                                                            |
   +===================================+========================================================================================================================================================================================+
   | table_name                        | Mandatory. Name of the Hudi table from which invalid data files are to be deleted.                                                                                                     |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | op_type                           | Optional. Command running mode. The default value is **dry_run**. Value options are **dry_run**, **repair**, **undo**, and **query**.                                                  |
   |                                   |                                                                                                                                                                                        |
   |                                   | **dry_run**: displays invalid data files to be cleaned.                                                                                                                                |
   |                                   |                                                                                                                                                                                        |
   |                                   | **repair**: displays and cleans invalid data files.                                                                                                                                    |
   |                                   |                                                                                                                                                                                        |
   |                                   | **undo**: restores deleted data files.                                                                                                                                                 |
   |                                   |                                                                                                                                                                                        |
   |                                   | **query**: displays the backup directories that have been cleaned.                                                                                                                     |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | backup_path                       | Mandatory. Backup directory of the data files to be restored. This parameter is available only when the running mode is **undo**.                                                      |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | start_time                        | Optional. Start time for generating invalid data files. This parameter is available only when the running mode is **dry_run** or **repair**. The start time is not limited by default. |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | end_time                          | Optional. End time for generating invalid data files. This parameter is available only when the running mode is **dry_run** or **repair**. The end time is not limited by default.     |
   +-----------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Example
-------

.. code-block::

   call clean_file(table => 'h1', mode=>'repair');
   call clean_file(table => 'h1', mode=>'dry_run');
   call clean_file(table => 'h1', mode=>'query');
   call clean_file(table => 'h1', mode=>'undo', backup_path=>'/tmp/hudi/h1/.hoodie/.cleanbackup/hoodie_repair_backup_20220222222222');

Precautions
-----------

The command cleans only invalid Parquet files.

System Response
---------------

You can view command execution results in the driver log or on the client.
