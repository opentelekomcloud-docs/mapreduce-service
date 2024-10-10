:original_name: admin_guide_000413.html

.. _admin_guide_000413:

Configuring ClickHouse SQL Inspection
=====================================

Scenario
--------

You can configure rules for ClickHouse SQL inspection on FusionInsight Manager and configure rule parameters as you need.

Prerequisites
-------------

-  The cluster client that contains the ClickHouse service has been installed in the **/opt/hadoopclient** directory.
-  The ClickHouse logical cluster is running properly.
-  For clusters with Kerberos authentication enabled, you need to create a service user who has the permission to operate the ClickHouse table. For example, create a human-machine user **clickhouseuser**.
-  A tenant associated with the ClickHouse service has been created and associated with the ClickHouse service user. For details, see :ref:`Creating Tenants <admin_guide_000100>`

Constraints
-----------

-  The default dynamic validity period of a rule is 1 minute.
-  Interception and blocking rules will interrupt SQL queries, so you need to set parameters of these rules properly based on the site requirements.
-  After configuring ClickHouse rules, you need to log in to the client again for the rules to take effect.

Procedure
---------

#. Log in to FusionInsight Manager, click **Cluster**, and choose **SQL Inspector**. The **SQL Inspector** page is displayed.

#. Add rules for ClickHouse by referring to :ref:`Adding an SQL Inspection <admin_guide_000409>`.

   For details about the rules supported by the ClickHouse SQL engine, see :ref:`MRS SQL Inspection Rules <admin_guide_000409__en-us_topic_0000001662442869_section19510043143814>`.

   For example, add a rule whose ID is **static_0008** and checks whether a SQL statement executes the cluster-level table update operation. If so, the system displays a hint.


   .. figure:: /_static/images/en-us_image_0000002007717733.png
      :alt: **Figure 1** Adding a ClickHouse SQL inspection rule

      **Figure 1** Adding a ClickHouse SQL inspection rule

#. Log in to the node where the ClickHouse client is installed and run the following command to switch to the client installation directory.

   **cd /opt/hadoopclient**

   Run the following command to set environment variables:

   **source bigdata_env**

#. If the current cluster is in security mode (Kerberos authentication is enabled), run the following command to authenticate the current user. The current user must have the permission to create ClickHouse tables. If the current cluster is in normal mode (Kerberos authentication is disabled), skip this step.

   **kinit** *Component service user*

   Example: **kinit clickhouseuser**

#. Use the ClickHouse client to connect to the ClickHouse server.

   Security mode

   **clickhouse client --host** *IP address of the ClickHouseServer instance* **--port** **9440** **--secure**

   Normal clusters:

   **clickhouse client --host** *IP address of the ClickHouseServer instance*\ **--user** *Username* **--password** **--port** **9000**

   *Enter the password.*

#. Run the following statements to create a data table:

   **CREATE DATABASE** *cktest* **ON CLUSTER** *default_cluster*\ **;**

   **CREATE TABLE** *cktest.test2* **ON CLUSTER** *default_cluster* **( \`EventDate\` DateTime, \`CounterID\` UInt32, \`UserID\` UInt32, \`ver\` UInt16 ) ENGINE = ReplicatedMergeTree('/clickhouse/tables/{shard}/**\ *cktest/test2*\ **', '{replica}')** **PARTITION BY toYYYYMM(EventDate) ORDER BY (EventDate, intHash32(UserID));**

   **CREATE TABLE** *cktest.test2_dir* **ON CLUSTER** *default_cluster* **as** *cktest.test2* **ENGINE = Distributed(**\ *default_cluster, cktest, test2*\ **, rand());**

#. Run the following command to insert data to the table:

   **insert into** *cktest.test2* **values('2023-08-01',111,111,111);**

   **insert into** *cktest.test2* **values('2023-08-02',222,111,111);**

#. Run the following SQL statement for the created table to check whether the rule takes effect:

   **alter table** *cktest.test2* **on cluster** *default_cluster* **update CounterID = toUInt32(222) where EventDate='2023-08-01' ;**

   .. code-block::

      ...
      <Warning> SQLDefender: Distributed DDL ALTER UPDATE queries are undesirable.
      ...

   If the operation set in the rule is **Intercept**, the statement fails to be executed and the following information is displayed:

   .. code-block::

      ...
      DB::Exception: Distributed DDL ALTER TABLE UPDATE queries are undesirable..(QUERY_IS_PROHIBITED)
      ...

   .. note::

      For more ClickHouse SQL inspection rules, see :ref:`MRS SQL Inspection Rules <admin_guide_000409__en-us_topic_0000001662442869_section19510043143814>`.
