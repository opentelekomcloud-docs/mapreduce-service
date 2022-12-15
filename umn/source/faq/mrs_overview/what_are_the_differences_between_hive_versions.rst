:original_name: mrs_03_1081.html

.. _mrs_03_1081:

What Are the Differences Between Hive Versions?
===============================================

Hive 3.1 has the following differences when compared with Hive 1.2:

-  String cannot be converted to int.
-  The user-defined functions (UDFs) of the **Date** type are changed to Hive built-in UDFs.
-  Hive 3.1 does not provide the index function anymore.
-  Hive 3.1 uses the UTC time in time functions, while Hive 1.2 uses the local time zone.
-  The JDBC drivers in Hive 3.1 and Hive 1.2 are incompatible.
-  In Hive 3.1, column names in ORC files are case-sensitive and underscores-sensitive.
-  Hive 3.1 does not allow columns named **time**.
