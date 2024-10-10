:original_name: mrs_01_2398.html

.. _mrs_01_2398:

Creating a ClickHouse Table
===========================

ClickHouse implements the replicated table mechanism based on the ReplicatedMergeTree engine and ZooKeeper. When creating a table, you can specify an engine to determine whether the table is highly available. Shards and replicas of each table are independent of each other.

ClickHouse also implements the distributed table mechanism based on the Distributed engine. Views are created on all shards (local tables) for distributed query, which is easy to use. ClickHouse has the concept of data sharding, which is one of the features of distributed storage. That is, parallel read and write are used to improve efficiency.

.. _mrs_01_2398__section1386435625:

Viewing cluster and Other Environment Parameters of ClickHouse
--------------------------------------------------------------

#. Use the ClickHouse client to connect to the ClickHouse server by referring to :ref:`Using ClickHouse from Scratch <mrs_01_2345>`.

#. .. _mrs_01_2398__li5153155032517:

   Query the cluster identifier and other information about the environment parameters.

   **select cluster,shard_num,replica_num,host_name from system.clusters;**

   .. code-block::

      SELECT
          cluster,
          shard_num,
          replica_num,
          host_name
      FROM system.clusters

      ┌─cluster───────────┬─shard_num─┬─replica_num─┬─host_name──────── ┐
      │ default_cluster_1             │         1   │           1   │ node-master1dOnG           │
      │ default_cluster_1             │         1   │           2   │ node-group-1tXED0001       │
      │ default_cluster_1             │         2   │           1   │ node-master2OXQS           │
      │ default_cluster_1             │         2   │           2   │ node-group-1tXED0002       │
      │ default_cluster_1             │         3   │           1   │ node-master3QsRI           │
      │ default_cluster_1             │         3   │           2   │ node-group-1tXED0003       │
      └─────────────── ┴────── ┴─────── ┴──────────────┘

      6 rows in set. Elapsed: 0.001 sec.

#. Query the shard and replica identifiers.

   **select \* from system.macros**;

   .. code-block::

      SELECT *
      FROM system.macros

      ┌─macro───┬─substitution─────┐
      │ id          │ 76                     │
      │ replica     │ node-master3QsRI       │
      │ shard       │ 3                      │
      └────── ┴────────────┘

      3 rows in set. Elapsed: 0.001 sec.

.. _mrs_01_2398__section1564103819477:

Creating a Local Replicated Table and a distributed Table
---------------------------------------------------------

#. Log in to the ClickHouse node using the client, for example, **clickhouse client --host** *node-master3QsRI* **--multiline --port 9440 --secure;**

   .. note::

      *node-master3QsRI* is the value of **host_name** obtained in :ref:`2 <mrs_01_2398__li5153155032517>` in :ref:`Viewing cluster and Other Environment Parameters of ClickHouse <mrs_01_2398__section1386435625>`.

#. .. _mrs_01_2398__li89698281356:

   Create a replicated table using the ReplicatedMergeTree engine.

   For details about the syntax, see https://clickhouse.tech/docs/en/engines/table-engines/mergetree-family/replication/#creating-replicated-tables.

   For example, run the following commands to create a ReplicatedMergeTree table named **test** on the **default_cluster_1** node and in the **default** database:

   **CREATE TABLE** *default.test* **ON CLUSTER** *default_cluster_1*

   **(**

   **\`EventDate\` DateTime,**

   **\`id\` UInt64**

   **)**

   **ENGINE = ReplicatedMergeTree('**\ */clickhouse/tables/{shard}/default/test*\ **', '**\ *{replica}*'**)**

   **PARTITION BY toYYYYMM(EventDate)**

   **ORDER BY id;**

   The parameters are described as follows:

   -  The **ON CLUSTER** syntax indicates the distributed DDL, that is, the same local table can be created on all instances in the cluster after the statement is executed once.
   -  **default_cluster_1** is the cluster identifier obtained in :ref:`2 <mrs_01_2398__li5153155032517>` in :ref:`Viewing cluster and Other Environment Parameters of ClickHouse <mrs_01_2398__section1386435625>`.

      .. caution::

         **ReplicatedMergeTree** engine receives the following two parameters:

         -  Storage path of the table data in ZooKeeper

            The path must be in the **/clickhouse** directory. Otherwise, data insertion may fail due to insufficient ZooKeeper quota.

            To avoid data conflict between different tables in ZooKeeper, the directory must be in the following format:

            */clickhouse/tables/{shard}*\ **/**\ *default/test*, in which **/clickhouse/tables/{shard}** is fixed, *default* indicates the database name, and *text* indicates the name of the created table.

         -  Replica name: Generally, **{replica}** is used.

   .. code-block::

      CREATE TABLE default.test ON CLUSTER default_cluster_1
      (
          `EventDate` DateTime,
          `id` UInt64
      )
      ENGINE = ReplicatedMergeTree('/clickhouse/tables/{shard}/default/test', '{replica}')
      PARTITION BY toYYYYMM(EventDate)
      ORDER BY id

      ┌─host─────────────────┬─port─┬─status─┬─error─┬─num_hosts_remaining─┬─num_hosts_active─┐
      │ node-group-1tXED0002                   │  9000  │      0   │         │                   5   │                3   │
      │ node-group-1tXED0003                   │  9000  │      0   │         │                   4   │                3   │
      │ node-master1dOnG                       │  9000  │      0   │         │                   3   │                3   │
      └────────────────────┴────┴─────┴──── ┴─────────── ┴──────────┘
      ┌─host─────────────────┬─port─┬─status─┬─error─┬─num_hosts_remaining─┬─num_hosts_active─┐
      │ node-master3QsRI                       │  9000  │      0   │         │                   2   │                0   │
      │ node-group-1tXED0001                   │  9000  │      0   │         │                   1   │                0   │
      │ node-master2OXQS                       │  9000  │      0   │         │                   0   │                0   │
      └────────────────────┴────┴─────┴──── ┴─────────── ┴──────────┘

      6 rows in set. Elapsed: 0.189 sec.

#. .. _mrs_01_2398__li16616143173215:

   Create a distributed table using the Distributed engine.

   For example, run the following commands to create a distributed table named **test_all** on the **default_cluster_1** node and in the **default** database:

   **CREATE TABLE** *default.test_all* **ON CLUSTER** *default_cluster_1*

   **(**

   **\`EventDate\` DateTime,**

   **\`id\` UInt64**

   **)**

   **ENGINE = Distributed(**\ *default_cluster_1, default, test, rand()*\ **);**

   .. code-block::

      CREATE TABLE default.test_all ON CLUSTER default_cluster_1
      (
          `EventDate` DateTime,
          `id` UInt64
      )
      ENGINE = Distributed(default_cluster_1, default, test, rand())

      ┌─host─────────────────┬─port─┬─status─┬─error─┬─num_hosts_remaining─┬─num_hosts_active─┐
      │ node-group-1tXED0002                   │  9000  │      0   │         │                   5   │                0   │
      │ node-master3QsRI                       │  9000  │      0   │         │                   4   │                0   │
      │ node-group-1tXED0003                   │  9000  │      0   │         │                   3   │                0   │
      │ node-group-1tXED0001                   │  9000  │      0   │         │                   2   │                0   │
      │ node-master1dOnG                       │  9000  │      0   │         │                   1   │                0   │
      │ node-master2OXQS                       │  9000  │      0   │         │                   0   │                0   │
      └────────────────────┴────┴─────┴──── ┴─────────── ┴──────────┘

      6 rows in set. Elapsed: 0.115 sec.

   .. note::

      **Distributed** requires the following parameters:

      -  **default_cluster_1** is the cluster identifier obtained in :ref:`2 <mrs_01_2398__li5153155032517>` in :ref:`Viewing cluster and Other Environment Parameters of ClickHouse <mrs_01_2398__section1386435625>`.

      -  **default** indicates the name of the database where the local table is located.

      -  **test** indicates the name of the local table. In this example, it is the name of the table created in :ref:`2 <mrs_01_2398__li89698281356>`.

      -  (Optional) Sharding key

         This key and the weight configured in the **config.xml** file determine the route for writing data to the distributed table, that is, the physical table to which the data is written. It can be the original data (for example, **site_id**) of a column in the table or the result of the function call, for example, **rand()** is used in the preceding SQL statement. Note that data must be evenly distributed in this key. Another common operation is to use the hash value of a column with a large difference, for example, **intHash64(user_id)**.

ClickHouse Table Data Operations
--------------------------------

#. Log in to the ClickHouse node on the client. Example:

   **clickhouse client --host** *node-master3QsRI* **--multiline --port 9440 --secure;**

   .. note::

      *node-master3QsRI* is the value of **host_name** obtained in :ref:`2 <mrs_01_2398__li5153155032517>` in :ref:`Viewing cluster and Other Environment Parameters of ClickHouse <mrs_01_2398__section1386435625>`.

#. .. _mrs_01_2398__li77990531075:

   After creating a table by referring to :ref:`Creating a Local Replicated Table and a distributed Table <mrs_01_2398__section1564103819477>`, you can insert data to the local table.

   For example, run the following command to insert data to the local table **test**:

   **insert into test values(toDateTime(now()), rand());**

#. Query the local table information.

   For example, run the following command to query data information of the table **test** in :ref:`2 <mrs_01_2398__li77990531075>`:

   **select \* from test;**

   .. code-block::

      SELECT *
      FROM test

      ┌───────────EventDate─┬─────────id─┐
      │ 2020-11-05 21:10:42             │ 1596238076           │
      └──────────────── ┴───────────┘

      1 rows in set. Elapsed: 0.002 sec.


#. Query the distributed table.

   For example, the distributed table **test_all** is created based on table **test** in :ref:`3 <mrs_01_2398__li16616143173215>`. Therefore, the same data in table **test** can also be queried in table **test_all**.

   **select \* from test_all;**

   .. code-block::

      SELECT *
      FROM test_all

      ┌───────────EventDate─┬─────────id─┐
      │ 2020-11-05 21:10:42             │ 1596238076           │
      └──────────────── ┴───────────┘

      1 rows in set. Elapsed: 0.004 sec.

#. Switch to the shard node with the same **shard_num** and query the information about the current table. The same table data can be queried.

   For example, run the **exit;** command to exit the original node.

   Run the following command to switch to the **node-group-1tXED0003** node:

   **clickhouse client --host** *node-group-1tXED0003* **--multiline --port 9440 --secure;**

   .. note::

      The **shard_num** values of **node-group-1tXED0003** and **node-master3QsRI** are the same by performing :ref:`2 <mrs_01_2398__li5153155032517>`.

   **show tables;**

   .. code-block::

      SHOW TABLES

      ┌─name─────┐
      │ test           │
      │ test_all       │
      └────────┘


#. Query the local table data. For example, run the following command to query data in table **test** on the **node-group-1tXED0003** node:

   **select \* from test;**

   .. code-block::

      SELECT *
      FROM test

      ┌───────────EventDate─┬─────────id─┐
      │ 2020-11-05 21:10:42             │ 1596238076           │
      └──────────────── ┴───────────┘

      1 rows in set. Elapsed: 0.005 sec.

#. Switch to the shard node with different **shard_num** value and query the data of the created table.

   For example, run the following command to exit the **node-group-1tXED0003** node:

   **exit;**

   Switch to the **node-group-1tXED0001** node. The **shard_num** values of **node-group-1tXED0001** and **node-master3QsRI** are different by performing :ref:`2 <mrs_01_2398__li5153155032517>`.

   **clickhouse client --host** *node-group-1tXED0001* **--multiline --port 9440 --secure;**

   Query the local table **test**. Data cannot be queried on the different shard node because table **test** is a local table.

   **select \* from test;**

   .. code-block::

      SELECT *
      FROM test

      Ok.

   Query data in the distributed table **test_all**. The data can be queried properly.

   **select \* from test_all;**

   .. code-block::

      SELECT *
      FROM test

      ┌───────────EventDate─┬─────────id─┐
      │ 2020-11-05 21:12:19             │ 3686805070           │
      └──────────────── ┴───────────┘

      1 rows in set. Elapsed: 0.002 sec.

