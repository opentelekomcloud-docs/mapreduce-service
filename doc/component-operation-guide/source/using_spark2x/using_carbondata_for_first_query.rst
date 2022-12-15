:original_name: mrs_01_2362.html

.. _mrs_01_2362:

Using CarbonData for First Query
================================

Tool Overview
-------------

The first query of CarbonData is slow, which may cause a delay for nodes that have high requirements on real-time performance.

The tool provides the following functions:

-  Preheat the tables that have high requirements on query delay for the first time.

Tool Usage
----------

Download and install the client. For example, the installation directory is **/opt/client**. Go to the **/opt/client/Spark2x/spark/bin** directory and run **start-prequery.sh**.

Configure **prequeryParams.properties** by referring to :ref:`Table 1 <mrs_01_2362__table1684114449372>`.

.. _mrs_01_2362__table1684114449372:

.. table:: **Table 1** Parameters

   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | Parameter                        | Description                                                                                                                                                                                                           | Example                                                                          |
   +==================================+=======================================================================================================================================================================================================================+==================================================================================+
   | spark.prequery.period.max.minute | Maximum preheating duration, in minutes.                                                                                                                                                                              | 60                                                                               |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | spark.prequery.tables            | Table name configuration, *database.table:int*. The table name supports the wildcard (``*``). **int** indicates the duration (unit: day) within which the table is updated before it is preheated.                    | default.test*:10                                                                 |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | spark.prequery.maxThreads        | Maximum number of concurrent threads during preheating                                                                                                                                                                | 50                                                                               |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | spark.prequery.sslEnable         | The value is **true** in security mode and **false** in non-security mode.                                                                                                                                            | true                                                                             |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | spark.prequery.driver            | IP address and port number of JDBCServer. The format is *IP address:Port number*. If multiple servers need to be preheated, enter multiple *IP address:Port number* of the servers and separate them with commas (,). | 192.168.0.2:22550                                                                |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | spark.prequery.sql               | SQL statement for preheating. Different statements are separated by colons (:).                                                                                                                                       | SELECT COUNT(``*``) FROM %s;SELECT \* FROM %s LIMIT 1                            |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+
   | spark.security.url               | URL required by JDBC in security mode                                                                                                                                                                                 | ;saslQop=auth-conf;auth=KERBEROS;principal=spark2x/hadoop.hadoop.com@HADOOP.COM; |
   +----------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+----------------------------------------------------------------------------------+

.. note::

   The statement configured in **spark.prequery.sql** is executed in each preheated table. The table name is replaced with **%s**.

**Script Usage**

Command format: **sh** **start-prequery.sh**

To run this command, place **user.keytab** or **jaas.conf** (either of them) and **krb5.conf** (mandatory) in the **conf** directory.

.. note::

   -  Currently, this tool supports only Carbon tables.
   -  This tool initializes the Carbon environment and pre-reads table metadata to JDBCServer. Therefore, this tool is more suitable for multi-active instances and static allocation mode.
