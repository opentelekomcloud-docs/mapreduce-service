:original_name: mrs_01_1470.html

.. _mrs_01_1470:

Why Missing Privileges Exception is Reported When I Perform Drop Operation on Databases?
========================================================================================

Question
--------

Why drop database cascade is throwing the following exception?

.. code-block::

   Error: org.apache.spark.sql.AnalysisException: Missing Privileges;(State=,code=0)

Answer
------

This error is thrown when the owner of the database performs **drop database <database_name> cascade** which contains tables created by other users.
