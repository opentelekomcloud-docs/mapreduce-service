:original_name: mrs_01_0389.html

.. _mrs_01_0389:

Deleting a CarbonData Table
===========================

Scenario
--------

Unused CarbonData tables can be deleted. After a CarbonData table is deleted, its metadata and loaded data are deleted together.

Procedure
---------

#. Run the following command to delete a CarbonData table:

   **DROP TABLE [IF EXISTS] [db_name.]table_name;**

   **db_name** is optional. If **db_name** is not specified, the table named **table_name** in the current database is deleted.

   For example, run the following command to delete the **productSalesTable** table in the **productdb** database:

   **DROP TABLE productdb.productSalesTable;**

#. Run the following command to confirm that the table is deleted:

   **SHOW TABLES;**
