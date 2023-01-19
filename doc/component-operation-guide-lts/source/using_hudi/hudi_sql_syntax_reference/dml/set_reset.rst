:original_name: mrs_01_24278.html

.. _mrs_01_24278:

SET/RESET
=========

Function
--------

This command is used to dynamically add, update, display, or reset Hudi parameters without restarting the driver.

Syntax
------

-  Add or update a parameter value:

   **SET** *parameter_name*\ =\ *parameter_value*

   This command is used to add or update the value of **parameter_name**.

-  Display a parameter value:

   **SET** *parameter_name*

   This command is used to display the value of **parameter_name**.

-  Display session parameters:

   **SET**

   This command is used to display all supported session parameters.

-  Display session parameters along with usage details:

   **SET** -v

   This command is used to display all supported session parameters and their usage details.

-  Reset parameter values:

   **RESET**

   This command is used to reset all session parameters.

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +-----------------+-----------------------------------------------------------------------+
   | Parameter       | Description                                                           |
   +=================+=======================================================================+
   | parameter_name  | Name of the parameter to be dynamically added, updated, or displayed. |
   +-----------------+-----------------------------------------------------------------------+
   | parameter_value | New value to be set for **parameter_name**.                           |
   +-----------------+-----------------------------------------------------------------------+

Precautions
-----------

The following table lists the properties to be used in the **SET** or **RESET** commands.

.. table:: **Table 2** Properties

   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | Property                               | Description                                                                                                                                                                            |
   +========================================+========================================================================================================================================================================================+
   | hoodie.insert.shuffle.parallelism      | Degree of parallelism (DOP) of Spark shuffle for writing data in insert mode.                                                                                                          |
   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hoodie.upsert.shuffle.parallelism      | DOP of Spark shuffle for writing data in upsert mode.                                                                                                                                  |
   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hoodie.delete.shuffle.parallelism      | DOP of Spark shuffle for deleting data in delete mode.                                                                                                                                 |
   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hoodie.sql.insert.mode                 | Insert mode. The value can be strict, non-strict, or upsert.                                                                                                                           |
   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | hoodie.sql.bulk.insert.enable          | Whether to enable bulk insert.                                                                                                                                                         |
   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
   | spark.sql.hive.convertMetastoreParquet | Converts the parquet table into a data source table for reading. If the provider of Hudi is Hive and Spark SQL or Spark Beeline is used to read data, set this parameter to **false**. |
   +----------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

Examples
--------

-  Add or Update command:

   .. code-block::

      set hoodie.insert.shuffle.parallelism = 100;
      set hoodie.upsert.shuffle.parallelism = 100;
      set hoodie.delete.shuffle.parallelism = 100;

-  Reset command:

   .. code-block::

      RESET

System Response
---------------

-  You can view the success result in driver logs.
-  You can view the failure result on the UI.
