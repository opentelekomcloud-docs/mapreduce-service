:original_name: mrs_01_1635.html

.. _mrs_01_1635:

Using a Secondary Index
=======================

Scenario
--------

HIndex enables HBase indexing based on specific column values, making the retrieval of data highly efficient and fast.

Constraints
-----------

-  Column families are separated by semicolons (;).

-  Columns and data types must be contained in square brackets ([]).

-  The column data type is specified by using -> after the column name.

-  If the column data type is not specified, the default data type (string) is used.

-  The number sign (#) is used to separate two index details.

-  The following is an optional parameter:

   -Dscan.caching: number of cached rows when the data table is scanned.

   The default value is set to 1000.

-  Indexes are created for a single region to repair damaged indexes.

   This function is not used to generate new indexes.

Procedure
---------

#. Install the HBase client. For details, see :ref:`Using an HBase Client <mrs_01_24041>`.

#. Go to the client installation directory, for example, **/opt/client**.

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster is in security mode, run the following command to authenticate the user. In normal mode, user authentication is not required.

   **kinit** *Component service user*

#. Run the following command to access HIndex:

   **hbase org.apache.hadoop.hbase.hindex.mapreduce.TableIndexer**

   .. table:: **Table 1** Common HIndex commands

      +----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Description                      | Command                                                                                                                                                                        |
      +==================================+================================================================================================================================================================================+
      | Add Index                        | TableIndexer-Dtablename.to.index=table1-Dindexspecs.to.add='IDX1=>cf1:[q1->datatype],[q2],[q3];cf2:[q1->datatype],[q2->datatype]#IDX2=>cf1:[q5]'                               |
      +----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Create Index                     | TableIndexer -Dtablename.to.index=table1 -Dindexnames.to.build='IDX1#IDX2'                                                                                                     |
      +----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Delete Index                     | TableIndexer -Dtablename.to.index=table1 -Dindexnames.to.drop='IDX1#IDX2'                                                                                                      |
      +----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Disable Index                    | TableIndexer -Dtablename.to.index=table1 -Dindexnames.to.disable='IDX1#IDX2'                                                                                                   |
      +----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Add and Create Index             | TableIndexer -Dtablename.to.index=table1 -Dindexspecs.to.add='IDX1=>cf1:[q1->datatype],[q2],[q3];cf2:[q1->datatype],[q2->datatype]#IDX2=>cf1:[q5] -Dindexnames.to.build='IDX1' |
      +----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Create Index for a Single Region | TableIndexer -Dtablename.to.index=table1 -Dregion.to.index=regionEncodedName -Dindexnames.to.build='IDX1#IDX2'                                                                 |
      +----------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      -  **IDX1**: indicates the index name.
      -  **cf1**: indicates the column family name.
      -  **q1**: indicates the column name.
      -  **datatype**: indicates the data type, including String, Integer, Double, Float, Long, Short, Byte and Char.
