:original_name: mrs_01_24057.html

.. _mrs_01_24057:

ClickHouse User and Permission Management
=========================================

User Permission Model
---------------------

ClickHouse user permission management enables unified management of users, roles, and permissions on each ClickHouse instance in the cluster. You can use the permission management module of the Manager UI to create users, create roles, and bind the ClickHouse access permissions. User permissions are controlled by binding roles to users.

Resource management: :ref:`Table 1 <mrs_01_24057__en-us_topic_0000001219230659_table858112220269>` lists the resources supported by ClickHouse permission management.

Resource permissions: :ref:`Table 2 <mrs_01_24057__en-us_topic_0000001219230659_table20282143414276>` lists the resource permissions supported by ClickHouse.

.. _mrs_01_24057__en-us_topic_0000001219230659_table858112220269:

.. table:: **Table 1** Permission management objects supported by ClickHouse

   ======== ============= ==============
   Resource Integration   Remarks
   ======== ============= ==============
   Database Yes (level 1) ``-``
   Table    Yes (level 2) ``-``
   View     Yes (level 2) Same as tables
   ======== ============= ==============

.. _mrs_01_24057__en-us_topic_0000001219230659_table20282143414276:

.. table:: **Table 2** Resource permission list

   ========== ==================== =====================================
   Resource   Available Permission Remarks
   ========== ==================== =====================================
   Database   CREATE               CREATE DATABASE/TABLE/VIEW/DICTIONARY
   Table/View SELECT/INSERT        ``-``
   ========== ==================== =====================================

Prerequisites
-------------

-  The ClickHouse and Zookeeper services are running properly.
-  When creating a database or table in the cluster, the **ON CLUSTER** statement is used to ensure that the metadata of the database and table on each ClickHouse node is the same.

.. note::

   After the permission is granted, it takes about 1 minute for the permission to take effect.

Adding the ClickHouse Role
--------------------------

#. Log in to Manager and choose **System** > **Permission** > **Role**. On the **Role** page, click **Create Role**.

   |image1|

#. On the **Create Role** page, specify **Role Name**. In the **Configure Resource Permission** area, click the cluster name. On the service list page that is displayed, click the ClickHouse service.

   Determine whether to create a role with ClickHouse administrator permission based on service requirements.

   .. note::

      -  The ClickHouse administrator has all the database operation permissions except the permissions to create, delete, and modify users and roles.
      -  Only the built-in user **clickhouse** of ClickHouse has the permission to manage users and roles.

   -  If yes, go to :ref:`3 <mrs_01_24057__en-us_topic_0000001219230659_li9365913184120>`.
   -  If no, go to :ref:`4 <mrs_01_24057__en-us_topic_0000001219230659_li13347154819413>`.

#. .. _mrs_01_24057__en-us_topic_0000001219230659_li9365913184120:

   Select **SUPER_USER_GROUP** and click **OK**.

#. .. _mrs_01_24057__en-us_topic_0000001219230659_li13347154819413:

   Click **ClickHouse Scope**. The ClickHouse database resource list is displayed. If you select **create**, the role has the create permission on the database.

   Determine whether to grant the permission based on the service requirements.

   -  If yes, click **OK**.
   -  If no, go to :ref:`5 <mrs_01_24057__en-us_topic_0000001219230659_li17964516204412>`.

#. .. _mrs_01_24057__en-us_topic_0000001219230659_li17964516204412:

   Click the resource name and select the *Database resource name to be operated*. On the displayed page, select **read** (SELECT permission) or **write** (INSERT permission) based on service requirements, and click **OK**.

Adding a User and Binding the ClickHouse Role to the User
---------------------------------------------------------

#. .. _mrs_01_24057__en-us_topic_0000001219230659_li1183214191540:

   Log in to Manager and choose **System** > **Permission** > **User** and click **Create**.

#. .. _mrs_01_24057__en-us_topic_0000001219230659_li0521154115455:

   Select **Human-Machine** for **User Type** and set **Password** and **Confirm Password** to the password of the user.

   .. note::

      -  Username: The username cannot contain hyphens (-). Otherwise, the authentication will fail.
      -  Password: The password cannot contain special characters $, ., and #. Otherwise, the authentication will fail.

#. In the **Role** area, click **Add**. In the displayed dialog box, select a role with the ClickHouse permission and click **OK** to add the role. Then, click **OK**.

#. Log in to the node where the ClickHouse client is installed and use the new username and password to connect to the ClickHouse service.

   a. Run the following command to go to the client installation directory. For example, the client installation directory is /opt/Bigdata/client.

      **cd /opt/client**

   b. Run the following command to configure environment variables:

      **source bigdata_env**

   c. If Kerberos authentication is enabled for the current cluster, run the following command to authenticate the current user. The user must have the permission to create ClickHouse tables. Therefore, you need to bind the corresponding role to the user. For details, see :ref:`ClickHouse User and Permission Management <mrs_01_24057>`. If Kerberos authentication is disabled for the current cluster, skip this step.

      **kinit** *Component service user*

      Example: **kinit clickhouseuser**

   d. Log in to the system as the new user.

      **clickhouse client --host** *IP address of the ClickHouse instance* **--user** *User added in :ref:`1 <mrs_01_24057__en-us_topic_0000001219230659_li1183214191540>`* **--password** *User password set in :ref:`2 <mrs_01_24057__en-us_topic_0000001219230659_li0521154115455>`* **--port** *ClickHouse port number*

Granting Permissions Using the Client in Abnormal Scenarios
-----------------------------------------------------------

By default, the table metadata on each node of the ClickHouse cluster is the same. Therefore, the table information on a random ClickHouse node is collected on the permission management page of Manager. If the **ON CLUSTER** statement is not used when databases or tables are created on some nodes, the resource may fail to be displayed during permission management, and permissions may not be granted to the resource. To grant permissions on the local table on a single ClickHouse node, perform the following steps on the background client.

.. note::

   The following operations are performed based on the obtained roles, database or table names, and IP addresses of the node where the corresponding ClickHouseServer instance is located.

   -  You can log in to FusionInsight Manager and choose **Cluster** > **Services** > **ClickHouse** > **Instance** to obtain the service IP address of the ClickHouseServer instance.
   -  System domain name: The default value is **hadoop.com**. Log in to FusionInsight Manager and choose **System** > **Permission** > **Domain and Mutual Trust**. The value of **Local Domain** is the system domain name. Change the letters to lowercase letters when running a command.

#. Log in to the node where the ClickHouseServer instance is located as user **root**.

#. .. _mrs_01_24057__en-us_topic_0000001219230659_li10408141903516:

   Run the following command to obtain the path of the **clickhouse.keytab** file:

   **ls ${BIGDATA_HOME}/FusionInsight_ClickHouse_*/install/FusionInsight-ClickHouse-*/clickhouse/keytab/clickhouse.keytab**

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to go to the client installation directory. For example, the client installation directory is /opt/Bigdata/client.

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to connect to the ClickHouseServer instance:

   If Kerberos authentication is enabled for the current cluster, run the following command:

   **clickhouse client --host** *IP address of the node where the ClickHouseServer instance is located* **--user clickhouse/hadoop.**\ *<System domain name>* **--password** *clickhouse.keytab path obtained in :ref:`2 <mrs_01_24057__en-us_topic_0000001219230659_li10408141903516>`* **--port** *ClickHouse port number* **--secure**

   If Kerberos authentication is disabled for the current cluster, run the following command:

   **clickhouse client --host** *IP address of the node where the ClickHouseServer instance is located* **--user clickhouse** **--port** *ClickHouse port number*

#. Run the following statement to grant permissions to a database:

   In the syntax for granting permissions, *DATABASE* indicates the name of the target database, and *role* indicates the target role.

   **GRANT** **[ON CLUSTER** *cluster_name*\ **]** *privilege* **ON** *{DATABASE|TABLE}* **TO** *{user \| role]*

   For example, grant user **testuser** the CREATE permission on database **t2**:

   **GRANT CREATE ON** *m2* **to** *testuser*\ **;**

#. Run the following commands to grant permissions on the table or view. In the following command, *TABLE* indicates the name of the table or view to be operated, and *user* indicates the role to be operated.

   Run the following command to grant the query permission on tables in a database:

   **GRANT SELECT ON** *TABLE* **TO** *user*\ **;**

   Run the following command to grant the write permission on tables in a database:

   **GRANT INSERT ON** *TABLE* **TO** *user*\ **;**

#. Run the following command to exit the client:

   **quit;**

.. |image1| image:: /_static/images/en-us_image_0000001387892350.png
