:original_name: mrs_01_1647.html

.. _mrs_01_1647:

Why Modified and Deleted Data Can Still Be Queried by Using the Scan Command?
=============================================================================

Question
--------

Why modified and deleted data can still be queried by using the **scan** command?

.. code-block::

   scan '<table_name>',{FILTER=>"SingleColumnValueFilter('<column_family>','column',=,'binary:<value>')"}

Answer
------

Because of the scalability of HBase, all values specific to the versions in the queried column are all matched by default, even if the values have been modified or deleted. For a row where column matching has failed (that is, the column does not exist in the row), the HBase also queries the row.

If you want to query only the new values and rows where column matching is successful, you can use the following statement:

.. code-block::

   scan '<table_name>',{FILTER=>"SingleColumnValueFilter('<column_family>','column',=,'binary:<value>',true,true)"}

This command can filter all rows where column query has failed. It queries only the latest values of the current data in the table; that is, it does not query the values before modification or the deleted values.

.. note::

   The related parameters of **SingleColumnValueFilter** are described as follows:

   SingleColumnValueFilter(final byte[] family, final byte[] qualifier, final CompareOp compareOp, ByteArrayComparable comparator, final boolean filterIfMissing, final boolean latestVersionOnly)

   Parameter description:

   -  family: family of the column to be queried.
   -  qualifier: column to be queried.
   -  compareOp: comparison operation, such as = and >.
   -  comparator: target value to be queried.
   -  filterIfMissing: whether a row is filtered out if the queried column does not exist. The default value is false.
   -  latestVersionOnly: whether values of the latest version are queried. The default value is false.
