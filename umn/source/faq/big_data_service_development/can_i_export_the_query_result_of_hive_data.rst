:original_name: mrs_03_1149.html

.. _mrs_03_1149:

Can I Export the Query Result of Hive Data?
===========================================

Run the following statement to export the query result of Hive data:

.. code-block::

   insert overwrite local directory "/tmp/out/" row format delimited fields terminated by "\t" select * from table;
