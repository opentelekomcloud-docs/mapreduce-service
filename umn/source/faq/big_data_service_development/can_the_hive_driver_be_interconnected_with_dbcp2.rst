:original_name: mrs_03_1049.html

.. _mrs_03_1049:

Can the Hive Driver Be Interconnected with DBCP2?
=================================================

The Hive driver cannot be interconnected with the DBCP2 database connection pool. The DBCP2 database connection pool invokes the **isValid** method to check whether a connection is available. However, Hive directly throws an exception when implementing this method.
