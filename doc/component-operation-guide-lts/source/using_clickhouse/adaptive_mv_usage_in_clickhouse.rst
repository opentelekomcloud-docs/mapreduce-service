:original_name: mrs_01_24287.html

.. _mrs_01_24287:

Adaptive MV Usage in ClickHouse
===============================

Scenario
--------

Materialized views (MVs) are used in ClickHouse to save the precomputed result of time-consuming operations. When querying data, you can query the materialized views rather than the original tables, thereby quickly obtaining the query result.

Currently, MVs are not easy to use in ClickHouse. Users can create one or more MVs based on the original table data as required. Once multiple MVs are created, you need to identify which MV is used and convert the query statement of an original table to that of an MV. In this way, the querying process is inefficient and prone to errors.

The problem mentioned above is readily solved since the adoption of adaptive MVs. When querying an original table, the corresponding MV of this table will be queried, which greatly improves the usability and efficiency of ClickHouse.

Matching Rules of Adaptive MVs
------------------------------

To ensure that the SQL statement for querying an original table can be automatically converted to that for querying the corresponding MV, the following matching rules must be met:

-  The table to be queried using an SQL statement must be associated with an MV.
-  The AggregatingMergeTree engine must be used with MVs.
-  Both the SELECT clause of SQL and MVs must contain aggregate functions.
-  If the SQL query contains a GROUP BY clause, MVs must also contain this clause.
-  If an MV contains a WHERE clause of SQL, the WHERE clause must be the same as that of the MV. This also applies to the PREWHERE and HAVING clauses.
-  Fields to be queried using the SQL statements must exist in the MVs.
-  If multiple MVs meet the preceding requirements, the SQL statement for querying the original table will be used.

For details about common matching failures of adaptive MVs, see :ref:`Common Matching Failures of MVs <mrs_01_24287__en-us_topic_0000001219029825_section332911341804>`.

Using Adaptive MVs
------------------

In the following operations, **local_table** is the original table and **view_table** is the MV created based on **local_table**. Change the table creation and query statements based on the site requirements.

#. Use the ClickHouse client to connect to the default database. For details, see :ref:`Using ClickHouse from Scratch <mrs_01_2345>`.

#. Run the following table creation statements to create the original table **local_table**.

   .. code-block::

      CREATE TABLE local_table
      (
      id String,
      city String,
      code String,
      value UInt32,
      create_time DateTime,
      age UInt32
      )
      ENGINE = MergeTree
      PARTITION BY toDate(create_time)
      ORDER BY (id, city, create_time);

#. Create the MV **view_table** based on **local_table**.

   .. code-block::

      CREATE MATERIALIZED VIEW view_table
      ENGINE = AggregatingMergeTree
      PARTITION BY toDate(create_time)
      ORDER BY (id, city, create_time)
      AS SELECT
      create_time,
      id,
      city,
      uniqState(code),
      sumState(value) AS value_new,
      minState(create_time) AS first_time,
      maxState(create_time) AS last_time
      FROM local_table
      WHERE create_time >= toDateTime('2021-01-01 00:00:00')
      GROUP BY id, city, create_time;

#. Insert data to the **local_table** table.

   .. code-block::

      INSERT INTO local_table values('1','zzz','code1',1,toDateTime('2021-01-02 00:00:00'), 10);
      INSERT INTO local_table values('2','kkk','code2',2,toDateTime('2020-01-01 00:00:00'), 20);
      INSERT INTO local_table values('3','ccc','code3',3,toDateTime('2022-01-01 00:00:00'), 30);

#. Run the following command to enable the adaptive MVs.

   .. code-block::

      set adaptive_materilized_view = 1;

   .. note::

      If the **adaptive_materilized_view** parameter is set to **1**, the adaptive MVs are enabled. If it is set to **0**, the adaptive MVs are disabled. The default value is **0**. **set adaptive_materilized_view = 1;** is a session-level command and needs to be reset each time the client connects to the server.

#. .. _mrs_01_24287__en-us_topic_0000001219029825_li1961113141710:

   Query data in the **local_table** table.

   .. code-block::

      SELECT sum(value)
      FROM local_table
      WHERE create_time >= toDateTime('2021-01-01 00:00:00')
      ┌─sumMerge(value_new)─┐
      │ 4 │
      └─────────────────────┘

#. Run the **explain syntax** command to view the execution plan of the SQL statement in step :ref:`6 <mrs_01_24287__en-us_topic_0000001219029825_li1961113141710>`. According to the query result, **view_table** is queried.

   .. code-block::

      EXPLAIN SYNTAX
      SELECT sum(value)
      FROM local_table
      WHERE create_time >= toDateTime('2021-01-01 00:00:00')
      ┌─explain────────────────────┐
      │ SELECT sumMerge(value_new) │
      │ FROM default.view_table    │
      └────────────────────────────┘

.. _mrs_01_24287__en-us_topic_0000001219029825_section332911341804:

Common Matching Failures of MVs
-------------------------------

-  When creating an MV, the aggregate functions must contain the State suffix. Otherwise, the corresponding MV cannot be matched. Example:

   .. code-block::

      # # The MV agg_view is created based on the original table test_table. However, the count aggregate function does not contain the State suffix.
      CREATE MATERIALIZED VIEW agg_view
      ENGINE = AggregatingMergeTree
      PARTITION BY toDate(create_time)
      ORDER BY (id)
      AS SELECT
      create_time,
      id,
      count(id)
      FROM test_table
      GROUP BY id,create_time;

      # To ensure that the MV can be matched, the count aggregate function for creating the MV must contain the State suffix. The correct example is as follows:
      CREATE MATERIALIZED VIEW agg_view
      ENGINE = AggregatingMergeTree
      PARTITION BY toDate(create_time)
      ORDER BY (id)
      AS SELECT
      create_time,
      id,
      countState(id)
      FROM test_table
      GROUP BY id,create_time;

-  Only if the WHERE clause of the statement for querying an original table is completely the same as that in an MV can the MV be matched.

   For example, if the WHERE clause of the original table statement is **where a=b** while the WHERE clause of the MV is **where b=a**, the corresponding MV cannot be matched.

   However, if the statement for querying the original table does not contain the database name, the corresponding MV can be matched. Example:

   .. code-block::

      # The MV view_test is created based on db_test.table_test. The WHERE clause for querying the original table contains the database name db_test.
      CREATE MATERIALIZED VIEW db_test.view_test ENGINE = AggregatingMergeTree ORDER BY phone AS
      SELECT
      name,
      phone,
      uniqExactState(class) as uniq_class,
      sumState(CRC32(phone))
      FROM db_test.table_test
      WHERE (class, name) GLOBAL IN
      (
      SELECT class, name FROM db_test.table_test
      WHERE
      name = 'zzzz'
      AND class = 'calss one'
      )
      GROUP BY
      name, phone;
      # If the WHERE clause does not contain the database name db_test, the corresponding MV will be matched.
      USE db_test;
      EXPLAIN SYNTAX
      SELECT
      name,
      phone,
      uniqExact(class) as uniq_class,
      sum(CRC32(phone))
      FROM table_test
      WHERE (class, name) GLOBAL IN
      (
      SELECT class, name FROM table_test
      WHERE
      name = 'zzzz'
      AND class = 'calss one'
      )
      GROUP BY
      name, phone;

-  If the GROUP BY clause contains functions, the corresponding MV can be matched only when the column field names in the functions are the same as those in an original table. Example:

   .. code-block::

      # Create the MV agg_view based on test_table.
      CREATE MATERIALIZED VIEW agg_view
      ENGINE = AggregatingMergeTree
      PARTITION BY toDate(create_time)
      ORDER BY (id, city, create_time)
      AS SELECT
      create_time,
      id,
      city,
      value as value1,
      uniqState(code),
      sumState(value) AS value_new,
      minState(create_time) AS first_time,
      maxState(create_time) AS last_time
      FROM test_table
      GROUP BY id, city, create_time, value1 % 2, value1;
      # The corresponding MV can be matched if the statement is as follows:
      SELECT uniq(code) FROM test_table GROUP BY id, city, value1 % 2;
      # The corresponding MV cannot be matched if the statement is as follows:
      SELECT uniq(code) FROM test_table GROUP BY id, city, value % 2;

-  In a created MV, the FROM clause cannot be a SELECT statement. Otherwise, the corresponding MV will fail to be matched. In the following example, the FROM clause is a SELECT statement. In this case, the corresponding MV cannot be matched.

   .. code-block::

      CREATE MATERIALIZED VIEW agg_view
      ENGINE = AggregatingMergeTree
      PARTITION BY toDate(create_time)
      ORDER BY (id)
      AS SELECT
      create_time,
      id,
      countState(id)
      FROM
      (SELECT id, create_time FROM test_table)
      GROUP BY id,create_time;

-  When querying original tables or creating MVs, an aggregate function cannot be used together with another aggregate function or a common function. Example:

   .. code-block::

      # Case 1: Multiple aggregate functions are used when querying an original table.
      # Create an MV.
      CREATE MATERIALIZED VIEW agg_view
      ENGINE = AggregatingMergeTree
      PARTITION BY toDate(create_time)
      ORDER BY (id)
      AS SELECT
      create_time,
      id,
      countState(id)
      FROM test_table
      GROUP BY id,create_time;
      # Two aggregate functions are used when querying the original table, leading to the MV matching failure.
      SELECT count(id) + count(id) FROM test_table;
      # Case 2: Multiple aggregate functions are used when creating an MV.
      # Two countState(id) functions are used when creating the MV, leading to the MV matching failure.
      CREATE MATERIALIZED VIEW agg_view
      ENGINE = AggregatingMergeTree
      PARTITION BY toDate(create_time)
      ORDER BY (id)
      AS SELECT
       create_time,
       id,
      (countState(id) + countState(id)) AS new_count
      FROM test_table
      GROUP BY id,create_time;
      # The corresponding MV cannot be matched when querying the original table.
      SELECT new_count FROM test_table;

   However, if the parameter of an aggregate function is the combination operation of fields, the corresponding MV can be matched.

   .. code-block::

      CREATE MATERIALIZED VIEW agg_view
      ENGINE = AggregatingMergeTree
      PARTITION BY toDate(create_time)
      ORDER BY (id)
      AS SELECT
      create_time,
      id,
      countState(id + id)
      FROM test_table
      GROUP BY id,create_time;
      # The corresponding MV can be matched when querying the original table.
      SELECT count(id + id) FROM test_table;
