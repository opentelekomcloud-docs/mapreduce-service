:original_name: mrs_01_0956.html

.. _mrs_01_0956:

Deleting Single-Row Records from Hive on HBase
==============================================

Scenario
--------

Due to the limitations of underlying storage systems, Hive does not support the ability to delete a single piece of table data. In Hive on HBase, MRS Hive supports the ability to delete a single piece of HBase table data. Using a specific syntax, Hive can delete one or more pieces of data from an HBase table.

.. table:: **Table 1** Permissions required for deleting single-row records from the Hive on HBase table

   =========================== ==========================
   Cluster Authentication Mode Required Permission
   =========================== ==========================
   Security mode               SELECT, INSERT, and DELETE
   Common mode                 None
   =========================== ==========================

Procedure
---------

#. To delete some data from an HBase table, run the following HQL statement:

   **remove table <table_name> where <expression>;**

   In the preceding information, *<expression>* specifies the filter condition of the data to be deleted. *<table_name>* indicates the Hive on HBase table from which data is to be deleted.
