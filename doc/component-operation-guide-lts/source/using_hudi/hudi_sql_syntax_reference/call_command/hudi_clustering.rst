:original_name: mrs_01_24802.html

.. _mrs_01_24802:

Hudi CLUSTERING
===============

Function
--------

Performs the clustering operation on Hudi tables. For details, see :ref:`Clustering <mrs_01_24088>`.

Syntax
------

-  Creating a savepoint:

   **call run_clustering(table=>'[table]', path=>'[path]', predicate=>'[predicate]', order=>'[order]');**

-  Performing clustering:

   **call show_clustering(table=>'[table]', path=>'[path]', limit=>'[limit]');**

Parameter Description
---------------------

.. table:: **Table 1** Parameters

   +-----------+-----------------------------------------------------------------------------------------+-----------+
   | Parameter | Description                                                                             | Mandatory |
   +===========+=========================================================================================+===========+
   | table     | Name of the table to be queried. The value can be in the **database.tablename** format. | No        |
   +-----------+-----------------------------------------------------------------------------------------+-----------+
   | path      | Path of the table to be queried                                                         | No        |
   +-----------+-----------------------------------------------------------------------------------------+-----------+
   | predicate | Predicate sentence to be defined                                                        | No        |
   +-----------+-----------------------------------------------------------------------------------------+-----------+
   | order     | Sorting field for clustering                                                            | No        |
   +-----------+-----------------------------------------------------------------------------------------+-----------+
   | limit     | Number of query results to display                                                      | No        |
   +-----------+-----------------------------------------------------------------------------------------+-----------+

Example
-------

.. code-block::

   call show_clustering(table => 'hudi_table1');

   call run_clustering(table => 'hudi_table1', predicate => '(ts >= 1006L and ts < 1008L) or ts >= 1009L', order => 'ts');

Precautions
-----------

Either **table** or **path** must exist. Otherwise, the Hudi table to be clustered cannot be determined.

System Response
---------------

You can view query results on the client.
