:original_name: mrs_03_1209.html

.. _mrs_03_1209:

How Do I Do If ClickHouse Consumes Excessive CPU Resources?
===========================================================

Symptom
-------

A user performs a large number of update operations using ClickHouse. This operation on a ClickHouse consumes a large number of resources. In addition, the operation will be executed again if it fails. As a result, retries of those failed operations occupy too many CPU resources.

Procedure
---------

Delete existing data from ZooKeeper and release delete the update statement.
