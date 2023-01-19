:original_name: mrs_01_2311.html

.. _mrs_01_2311:

Hive Materialized View
======================

Introduction
------------

A Hive materialized view is a special table obtained based on the query results of Hive internal tables. A materialized view can be considered as an intermediate table that stores actual data and occupies physical space. The tables on which a materialized view depends are called the base tables of the materialized view.

Materialized views are used to pre-compute and save the results of time-consuming operations such as table joining or aggregation. When executing a query, you can rewrite the query statement based on the base tables to the query statement based on materialized views. In this way, you do not need to perform time-consuming operations such as join and group by, thereby quickly obtaining the query result.

.. note::

   -  A materialized view is a special table that stores actual data and occupies physical space.
   -  Before deleting a base table, you must delete the materialized view created based on the base table.
   -  The materialized view creation statement is atomic, which means that other users cannot see the materialized view until all query results are populated.
   -  A materialized view cannot be created based on the query results of another materialized view.
   -  A materialized view cannot be created based on the results of a tableless query.
   -  You cannot insert, update, delete, load, or merge materialized views.
   -  You can perform complex query operations on materialized views, because they are special tables in nature.
   -  When the data of a base table is updated, you need to manually update the materialized view. Otherwise, the materialized view will retain the old data. That is, the materialized view expires.
   -  You can use the describe syntax to check whether the materialized view created based on ACID tables has expired.
   -  The describe statement cannot be used to check whether a materialized view created based on non-ACID tables has expired.

Creating a Materialized View
----------------------------

**Syntax**

.. code-block::

   CREATE MATERIALIZED VIEW [IF NOT EXISTS] [db_name.]materialized_view_name
     [COMMENT materialized_view_comment]
     DISABLE REWRITE
       [ROW FORMAT row_format]
       [STORED AS file_format]
         | STORED BY 'storage.handler.class.name' [WITH SERDEPROPERTIES (...)]
     ]
     [LOCATION hdfs_path]
     [TBLPROPERTIES (property_name=property_value, ...)]
   AS
   <query>;

.. note::

   -  Currently, the following materialized view file formats are supported: PARQUET, TextFile, SequenceFile, RCfile, and ORC. If **STORED AS** is not specified in the creation statement, the default file format is ORC.
   -  Names of materialized views must be unique in the same database. Otherwise, you cannot create a new materialized view, and data files of the original materialized view will be overwritten by the data files queried based on the base table in the new one. As a result, data may be tampered with. (After being tampered with, the materialized view can be restored by re-creating the materialized view.).

**Cases**

#. Log in to the Hive client and run the following command to enable the following parameters. For details, see :ref:`Using a Hive Client <mrs_01_0952>`.

   **set hive.support.concurrency=true;**

   **set hive.exec.dynamic.partition.mode=nonstrict;**

   **set hive.txn.manager=org.apache.hadoop.hive.ql.lockmgr.DbTxnManager;**

#. Create a base table and insert data.

   .. code-block::

      create table tb_emp(
      empno int,ename string,job string,mgr int,hiredate TIMESTAMP,sal float,comm float,deptno int
      )stored as orc
      tblproperties('transactional'='true');

      insert into tb_emp values(7369, 'SMITH', 'CLERK',7902, '1980-12-17 08:30:09',800.00,NULL,20),
      (7499, 'ALLEN', 'SALESMAN',7698, '1981-02-20 17:12:00',1600.00,300.00,30),
      (7521, 'WARD', 'SALESMAN',7698, '1981-02-22 09:05:34',1250.00,500.00,30),
      (7566, 'JONES', 'MANAGER', 7839, '1981-04-02 10:14:13',2975.00,NULL,20),
      (7654, 'MARTIN', 'SALESMAN',7698, '1981-09-28 08:36:17',1250.00,1400.00,30),
      (7698, 'BLAKE', 'MANAGER',7839, '1981-05-01 11:12:55',2850.00,NULL,30),
      (7782, 'CLARK', 'MANAGER',7839, '1981-06-09 15:45:28',2450.00,NULL,10),
      (7788, 'SCOTT', 'ANALYST',7566, '1987-04-19 14:05:34',3000.00,NULL,20),
      (7839, 'KING', 'PRESIDENT',NULL, '1981-11-17 10:18:25',5000.00,NULL,10),
      (7844, 'TURNER', 'SALESMAN',7698, '1981-09-08 09:05:34',1500.00,0.00,30),
      (7876, 'ADAMS', 'CLERK',7788, '1987-05-23 15:07:44',1100.00,NULL,20),
      (7900, 'JAMES', 'CLERK',7698, '1981-12-03 16:23:56',950.00,NULL,30),
      (7902, 'FORD', 'ANALYST',7566, '1981-12-03 08:48:17',3000.00,NULL,20),
      (7934, 'MILLER', 'CLERK',7782, '1982-01-23 11:45:29',1300.00,NULL,10);

#. Create a materialized view based on the results of the **tb_emp** query.

   .. code-block::

      create materialized view group_mv disable rewrite
      row format serde 'org.apache.hadoop.hive.serde2.JsonSerDe'
      stored as textfile
      tblproperties('mv_content'='Total compensation of each department')
      as select deptno,sum(sal) sum_sal from tb_emp group by deptno;

Applying a Materialized View
----------------------------

Rewrite the query statement based on base tables to the query statement based on materialized views to improve the query efficiency.

**Cases**

Execute the following query statement:

**select deptno,sum(sal) from tb_emp group by deptno having sum(sal)>10000;**

Based on the created materialized view, rewrite the query statement:

**select deptno, sum_sal from group_mv where sum_sal>10000;**

Checking a Materialized View
----------------------------

**Syntax**

**SHOW MATERIALIZED VIEWS [IN database_name] ['identifier_with_wildcards'];**

**DESCRIBE [EXTENDED \| FORMATTED] [db_name.]materialized_view_name;**

**Cases**

**show materialized views;**

**describe formatted group_mv;**

Deleting a Materialized View
----------------------------

**Syntax**

**DROP MATERIALIZED VIEW [db_name.]materialized_view_name;**

**Cases**

**drop materialized view group_mv;**

Rebuilding a Materialized View
------------------------------

When a materialized view is created, the base table data is filled in the materialized view. However, the data that is added, deleted, or modified in the base table is not automatically synchronized to the materialized view. Therefore, you need to manually rebuild the view after updating the data.

**Syntax**

**ALTER MATERIALIZED VIEW [db_name.]materialized_view_name REBUILD;**

**Cases**

**alter materialized view group_mv rebuild;**

.. note::

   When the base table data is updated but the materialized view data is not updated, the materialized view is in the expired state by default.

   The describe statement can be used to check whether a materialized view created based on transaction tables has expired. If the value of **Outdated for Rewriting** is **Yes**, the license has expired. If the value of **Outdated for Rewriting** is **No**, the license has not expired.
