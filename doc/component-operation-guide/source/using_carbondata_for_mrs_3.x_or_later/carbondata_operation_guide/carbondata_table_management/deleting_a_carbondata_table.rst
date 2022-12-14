:original_name: mrs_01_1410.html

.. _mrs_01_1410:

Deleting a CarbonData Table
===========================

Scenario
--------

You can run the **DROP TABLE** command to delete a table. After a CarbonData table is deleted, its metadata and loaded data are deleted together.

Procedure
---------

Run the following command to delete a CarbonData table:

Run the following command:

**DROP TABLE** *[IF EXISTS] [db_name.]table_name;*

Once this command is executed, the table is deleted from the system. In the command, **db_name** is an optional parameter. If **db_name** is not specified, the table named **table_name** in the current database is deleted.

Example:

**DROP TABLE** *productdb.productSalesTable;*

Run the preceding command to delete the **productSalesTable** table from the **productdb** database.

Operation Result
----------------

Deletes the table specified in the command from the system. After the table is deleted, you can run the **SHOW TABLES** command to check whether the table is successfully deleted. For details, see :ref:`SHOW TABLES <mrs_01_1428>`.
