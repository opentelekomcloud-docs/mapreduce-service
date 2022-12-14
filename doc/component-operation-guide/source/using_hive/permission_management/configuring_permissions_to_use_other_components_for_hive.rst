:original_name: mrs_01_0951.html

.. _mrs_01_0951:

Configuring Permissions to Use Other Components for Hive
========================================================

Scenario
--------

Hive may need to be associated with other components. For example, Yarn permissions are required in the scenario of using HQL statements to trigger MapReduce jobs, and HBase permissions are required in the Hive over HBase scenario. The following describes the operations in the two scenarios.

.. note::

   -  In security mode, Yarn and HBase permission management is enabled by default. Therefore, Yarn and HBase permissions need to be configured by default.
   -  In common mode, Yarn and HBase permission management is disabled by default. That is, any user has permissions. Therefore, YARN and HBase permissions does not need to be configured by default. If a user enables the permission management by modifying the Yarn or HBase configurations, the Yarn and HBase permissions then need to be configured.
   -  MRS 3.\ *x* or later supports Ranger. If the current component uses Ranger for permission control, you need to configure permission management policies based on Ranger. For details, see :ref:`Adding a Ranger Access Permission Policy for Hive <mrs_01_1858>`.

Prerequisites
-------------

-  The Hive client has been installed. For example, the installation directory is **/opt/client**.
-  You have obtained a user account with the system administrator permissions, such as **admin**.

Procedure
---------

**Association with Yarn in MRS Earlier than 3.x**

Yarn permissions are required when HQL statements, such as **insert**, **count**, **distinct**, **group by**, **order by**, **sort by**, and **join**, are used to trigger MapReduce jobs. The following uses the procedure for assigning a role the permissions to run the **count** statements in the **thc** table as an example.

#. Create a role on MRS Manager.
#. In the **Permission** table, choose **Yarn** > **Scheduler Queue** > **root**.
#. In the **Permission** column of the default queue, select **Submit** and click **OK**.
#. In the **Permission** table, choose **Hive** > **Hive Read Write Privileges** > **default**, select **Select** for **thc**, and click **OK**.

**Association with** **Yarn** **in MRS 3.\ x or Later**

Yarn permissions are required when HQL statements, such as **insert**, **count**, **distinct**, **group by**, **order by**, **sort by**, and **join**, are used to trigger MapReduce jobs. The following uses the procedure for assigning a role the permissions to run the **count** statements in the **thc** table as an example.

#. Create a role on FusionInsight Manager.
#. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Yarn** > **Scheduler Queue** > **root**.
#. In the **Permission** column of the **default** queue, select **Submit** and click **OK**.
#. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Hive** > **Hive Read Write Privileges** > **default**. Select **SELECT** for table **thc**, and click **OK**.

**Hive over HBase Authorization in MRS Earlier than 3.x**

After the permissions are assigned, you can use HQL statements that are similar to SQL statements to access HBase tables from Hive. The following uses the procedure for assigning a user the rights to query HBase tables as an example.

#. On the role management page of MRS Manager, create an HBase role, for example, **hive_hbase_create**, and grant the permission to create HBase tables.

   In the **Permission** table, choose **HBase** > **HBase Scope** > **global**, select **create** of the namespace **default**, and click **OK**.

#. On MRS Manager, create a human-machine user, for example, **hbase_creates_user**, add the user to the **hive** group, and bind the **hive_hbase_create** role to the user so that the user can create Hive and HBase tables.

#. Log in to the node where the client is installed. For details, see `Installing a Client <https://docs.otc.t-systems.com/usermanual/mrs/mrs_01_0091.html>`__.

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

#. Run the following command to authenticate the user:

   **kinit hbase_creates_user**

#. Run the following command to go to the shell environment of the Hive client:

   **beeline**

#. Run the following command to create a table in Hive and HBase, for example, the **thh** table.

   **CREATE TABLE thh(id int, name string, country string) STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler' WITH SERDEPROPERTIES("hbase.columns.mapping" = "cf1:id,cf1:name,:key") TBLPROPERTIES ("hbase.table.name" = "thh");**

   The created Hive table and the HBase table are stored in the Hive database **default** and the HBase namespace **default**, respectively.

#. On the role management page of MRS Manager, create a role, for example, **hive_hbase_select**, and assign the role the permission to query the Hive table **thh** and the HBase table **thh**.

   a. In the **Permission** table, choose **HBase** > **HBase Scope** > **global** > **default**, select **Read** for the **thh** table, and click **OK** to grant the HBase role the permission to query the table.
   b. Edit a role. In the **Permission** table, choose **HBase** > **HBase Scope** > **global** > **hbase**. Select **Execute** for **hbase:meta**, and click **OK**.
   c. Edit a role. In the **Permission** table, choose **Hive** > **Hive Read Write Privileges** > **default**, select **Select** for **thh**, and click **OK**.

#. On MRS Manager, create a human-machine user, for example, **hbase_select_user**, add the user to the **hive** group, and bind the **hive_hbase_select** role to the user so that the user can query Hive and HBase tables.

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

#. Run the following command to authenticate users:

   **kinit hbase_select_user**

#. Run the following command to go to the shell environment of the Hive client:

   **beeline**

#. Run the following command to use an HQL statement to query HBase table data:

   **select \* from thh;**

**Hive over HBase Authorization in MRS 3.\ x or Later**

After the permissions are assigned, you can use HQL statements that are similar to SQL statements to access HBase tables from Hive. The following uses the procedure for assigning a user the rights to query HBase tables as an example.

#. On the role management page of FusionInsight Manager, create an HBase role, for example, **hive_hbase_create**, and grant the permission to create HBase tables.

   In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **HBase** > **HBase Scope** > **global**. Select **Create** of the namespace **default**, and click **OK**.

#. On FusionInsight Manager, create a human-machine user, for example, **hbase_creates_user**, add the user to the **hive** group, and bind the **hive_hbase_create** role to the user so that the user can create Hive and HBase tables.

#. If the current component uses Ranger for permission control, grant the create permission for **hive_hbase_create** or **hbase_creates_user**. For details, see :ref:`Adding a Ranger Access Permission Policy for Hive <mrs_01_1858>`.

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

#. Run the following command to authenticate the user:

   **kinit hbase_creates_user**

#. Run the following command to go to the shell environment of the Hive client:

   **beeline**

#. Run the following command to create a table in Hive and HBase, for example, the **thh** table.

   **CREATE TABLE thh(id int, name string, country string) STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler' WITH SERDEPROPERTIES("hbase.columns.mapping" = "cf1:id,cf1:name,:key") TBLPROPERTIES ("hbase.table.name" = "thh");**

   The created Hive table and the HBase table are stored in the Hive database **default** and the HBase namespace **default**, respectively.

#. On the role management page of FusionInsight Manager, create a role, for example, **hive_hbase_select**, and assign the role the permission to query the Hive table **thh** and the HBase table **thh**.

   a. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **HBase** > **HBase Scope** > **global** > **default**. Select **read** of the **thh** table, and click **OK** to grant the table query permission to the HBase role.
   b. Edit the role. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **HBase** > **HBase Scope** > **global** > **hbase**, select **Execute** for **hbase:meta**, and click **OK**.
   c. Edit the role. In the **Configure Resource Permission** table, choose *Name of the desired cluster* > **Hive** > **Hive Read Write Privileges** > **default**. Select **SELECT** for the **thh** table, and click **OK**.

#. On FusionInsight Manager, create a human-machine user, for example, **hbase_select_user**, add the user to the **hive** group, and bind the **hive_hbase_select** role to the user so that the user can query Hive and HBase tables.

#. Run the following command to configure environment variables:

   **source /opt/client/bigdata_env**

#. Run the following command to authenticate users:

   **kinit hbase_select_user**

#. Run the following command to go to the shell environment of the Hive client:

   **beeline**

#. Run the following command to use an HQL statement to query HBase table data:

   **select \* from thh;**
