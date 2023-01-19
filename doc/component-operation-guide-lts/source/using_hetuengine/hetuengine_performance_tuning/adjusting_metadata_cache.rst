:original_name: mrs_01_1746.html

.. _mrs_01_1746:

Adjusting Metadata Cache
========================

Scenario
--------

When HetuEngine accesses the Hive data source, it needs to access the Hive metastore to obtain the metadata information. HetuEngine provides the metadata cache function. When the database or table of the Hive data source is accessed for the first time, the metadata information (database name, table name, table field, partition information, and permission information) of the database or table is cached, the Hive metastore does not need to be accessed again during subsequent access. If the table data of the Hive data source does not change frequently, the query performance can be improved to some extent.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **Cluster** > **Services** > **HetuEngine** > **Configurations** > **All Configurations** and adjust the metadata cache parameters by referring to :ref:`Table 1 <mrs_01_1746__en-us_topic_0000001173630766_table1201657173018>`.

   .. _mrs_01_1746__en-us_topic_0000001173630766_table1201657173018:

   .. table:: **Table 1** Metadata cache parameters

      +---------------------------------------------------+----------------------------------------------------------------------------------------------+---------------+-----------------+
      | Parameter                                         | Description                                                                                  | Default Value | Parameter File  |
      +===================================================+==============================================================================================+===============+=================+
      | hive.metastore-cache-ttl                          | Cache duration of the metadata of the co-deployed Hive data source.                          | 0s            | hive.properties |
      +---------------------------------------------------+----------------------------------------------------------------------------------------------+---------------+-----------------+
      | hive.metastore-cache-maximum-size                 | Maximum cache size of the metadata of the co-deployed Hive data source.                      | 10000         | hive.properties |
      +---------------------------------------------------+----------------------------------------------------------------------------------------------+---------------+-----------------+
      | hive.metastore-refresh-interval                   | Interval for refreshing the metadata of the co-deployed Hive data source.                    | 1s            | hive.properties |
      +---------------------------------------------------+----------------------------------------------------------------------------------------------+---------------+-----------------+
      | hive.per-transaction-metastore-cache-maximum-size | Maximum cache size of the metadata for each transaction of the co-deployed Hive data source. | 1000          | hive.properties |
      +---------------------------------------------------+----------------------------------------------------------------------------------------------+---------------+-----------------+

#. Click **Save**.

#. Choose **Cluster** > **Services** > **HetuEngine** > **More** > **Restart Service** to restart the HetuEngine service for the parameters to take effect.
