:original_name: mrs_01_2024.html

.. _mrs_01_2024:

Why Spark SQL Is Displayed as a Temporary Table in Different Databases?
=======================================================================

Question
--------

Why temporary tables of the previous database are displayed after the database is switched?

#. Create a temporary DataSource table, for example:

   .. code-block::

      create temporary table ds_parquet
      using org.apache.spark.sql.parquet
      options(path '/tmp/users.parquet');

#. Switch to another database, and run **show tables**. The temporary table created in the previous table is displayed.

   .. code-block::

      0: jdbc:hive2://192.168.169.84:22550/default> show tables;
      +-----------------+--------------+--+
      |    tableName    | isTemporary  |
      +-----------------+--------------+--+
      | ds_parquet      | true         |
      | cmb_tbl_carbon  | false        |
      +-----------------+--------------+--+
      2 rows selected (0.109 seconds)
      0: jdbc:hive2://192.168.169.84:22550/default>

Answer
------

The table management hierarchy of Spark is shown in :ref:`Figure 1 <mrs_01_2024__en-us_topic_0000001219351071_fa8229aa6660f4ac789ff2821c92b06a2>`. The lowest layer stores all temporary DataSource tables. There is no such concept as database at this layer. DataSource tables are visible in various databases.

The MetaStore of Hive is located at the upper layer. This layer distinguishes among databases. In each database, there are two types of Hive table, permanent and temporary. Therefore, Spark supports data tables of the same name at three layers.

During query, SparkSQL first checks for temporary Spark tables, then temporary Hive tables in the current database, and at last the permanent tables in the current database.

.. _mrs_01_2024__en-us_topic_0000001219351071_fa8229aa6660f4ac789ff2821c92b06a2:

.. figure:: /_static/images/en-us_image_0000001349139717.png
   :alt: **Figure 1** Spark table management hierarchy

   **Figure 1** Spark table management hierarchy

When a session quits, temporary tables related to the user operation are automatically deleted. Manual deletion of temporary files is not recommended.

When deleting temporary files, use the same priority as that for query. The priorities are temporary Spark table, temporary Hive table, and permanent Hive table ranging from high to low. If you want to directly delete Hive tables but not temporary Spark tables, you can directly use the **drop table DbName.TableName** command.
