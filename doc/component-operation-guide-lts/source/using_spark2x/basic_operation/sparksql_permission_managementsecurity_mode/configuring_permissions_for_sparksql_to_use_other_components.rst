:original_name: mrs_01_1939.html

.. _mrs_01_1939:

Configuring Permissions for SparkSQL to Use Other Components
============================================================

Scenario
--------

SparkSQL may need to be associated with other components. For example, Spark on HBase requires HBase permissions. The following describes how to associate SparkSQL with HBase.

Prerequisites
-------------

-  The Spark client has been installed. For example, the installation directory is **/opt/client**.
-  You have obtained a user account with the system administrator permissions, such as **admin**.

Procedure
---------

-  **Spark on HBase authorization**

   After the permissions are assigned, you can use statements that are similar to SQL statements to access HBase tables from SparkSQL. The following uses the procedure for assigning a user the permissions to query HBase tables as an example.

   .. note::

      Set **spark.yarn.security.credentials.hbase.enabled** to **true**.

   #. On Manager, create a role, for example, **hive_hbase_create**, and grant the permission to create HBase tables to the role.

      In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **HBase** > **HBase Scope** > **global**. Select **create** of the namespace **default**, and click **OK**.

      .. note::

         In this example, the created table is saved in the default database of Hive and has the CREATE permission of the default database. If you save the table to a Hive database other than **default**, perform the following operations:

         In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Hive** > **Hive Read Write Privileges**, select **CREATE** for the desired database, and click **OK**.

   #. On Manager, create a role, for example, **hive_hbase_submit**, and grant the permission to submit tasks to the Yarn queue.

      In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Yarn** > **Scheduling Queue** > **root**. Select **Submit** of **default**, and click **OK**.

   #. On Manager, create a human-machine user, for example, **hbase_creates_user**, add the user to the **hive** group, and bind the **hive_hbase_create** and **hive_hbase_submit** roles to create SparkSQL and HBase tables.

   #. Log in to the node where the client is installed as the client installation user.

   #. Run the following command to configure environment variables:

      **source /opt/client/bigdata_env**

      **source /opt/client/Spark2x/component_env**

   #. Run the following command to authenticate the user:

      **kinit hbase_creates_user**

   #. Run the following commands to enter the shell environment on the Spark JDBCServer client:

      **/opt/client/Spark2x/spark/bin/beeline -u "jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;user.principal=spark2x/hadoop.**\ *<system domain name>*\ **@**\ *<system domain name>*\ **;saslQop=auth-conf;auth=KERBEROS;principal=spark2x/hadoop.**\ *<system domain name>*\ **@**\ *<system domain name>*\ **;"**

   #. Run the following command to create a table in SparkSQL and HBase, for example, create the **hbaseTable** table:

      **create table hbaseTable (id string, name string, age int) using org.apache.spark.sql.hbase.HBaseSource options (hbaseTableName "table1", keyCols "id", colsMapping = ", name=cf1.cq1, age=cf1.cq2");**

      The created SparkSQL table and the HBase table are stored in the Hive database **default** and the HBase namespace **default**, respectively.

   #. On Manager, create a role, for example, **hive_hbase_select**, and grant the role the permission to query SparkSQL on HBase table **hbaseTable** and HBase table **hbaseTable**.

      -  In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **HBase** > **HBase Scope** > **global** > **default**. Select **read** for the **hbaseTable** table, and click **OK** to grant the table query permission to the HBase role.
      -  Edit the role. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **HBase** > **HBase Scope** > **global** > **hbase**. Select **Execute** for **hbase:meta**, and click **OK**.
      -  Edit the role. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Hive** > **Hive Read Write Privileges** > **default**. Select **SELECT** for the **hbaseTable** table, and click **OK**.

   #. On Manager, create a human-machine user, for example, **hbase_select_user**, add the user to the **hive** group, and bind the **hive_hbase_select** role to the user for querying SparkSQL and HBase tables.

   #. Run the following command to configure environment variables:

      **source /opt/client/bigdata_env**

      **source /opt/client/Spark2x/component_env**

   #. Run the following command to authenticate users:

      **kinit hbase_select_user**

   #. Run the following commands to enter the shell environment on the Spark JDBCServer client:

      **/opt/client/Spark2x/spark/bin/beeline -u "jdbc:hive2://<zkNode1_IP>:<zkNode1_Port>,<zkNode2_IP>:<zkNode2_Port>,<zkNode3_IP>:<zkNode3_Port>/;serviceDiscoveryMode=zooKeeper;zooKeeperNamespace=sparkthriftserver2x;user.principal=spark2x/hadoop.**\ *<system domain name>*\ **@**\ *<system domain name>*\ **;saslQop=auth-conf;auth=KERBEROS;principal=spark2x/hadoop.**\ *<system domain name>*\ **@**\ *<system domain name>*\ **;"**

   #. Run the following command to use a SparkSQL statement to query HBase table data:

      **select \* from thh;**
