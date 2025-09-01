:original_name: admin_guide_000427.html

.. _admin_guide_000427:

Configuring Doris SQL Inspection
================================

This function applies only to clusters of MRS 3.5.0 and later versions.

Scenario
--------

You can configure inspection rules for Doris SQL statements on MRS Manager and set rule parameters based on your needs.

Prerequisites
-------------

-  The node to be connected to the Doris database can communicate with the MRS cluster.
-  FE and BE instances are normal.
-  The MySQL client has been installed.

Constraints
-----------

-  A SQL inspection rule is automatically applied in 5 minutes.
-  Interception and blocking rules will interrupt SQL queries, so you need to set parameters of these rules properly based on the site requirements.

Procedure
---------

#. .. _admin_guide_000427__li141114717911:

   Create a user with the Doris administrator permissions to connect to the Doris service.

   a. Log in to MRS Manager as user **admin**, choose **System** > **Permission** > **Role**, click **Create Role**, set the following parameters, and click **OK**.

      -  **Role Name**: Enter a role name, for example, **dorisrole**.
      -  **Configure Resource Permission**: In the resource permission list, choose *Name of the target cluster* > **Doris** and select **Doris Administrator Permission** according to the permission you need. Click **Doris Read and Write Privileges** and select **Select**, **Drop**, **Load**, **Alter**, **Create**, and **Grant** permission in the **internal** row.


      .. figure:: /_static/images/en-us_image_0000002413536053.png
         :alt: **Figure 1** Creating a Doris role

         **Figure 1** Creating a Doris role

   b. Click **User**. If Kerberos authentication is enabled for the cluster (the cluster is in security mode), add a human-machine user. If Kerberos authentication is disabled for the cluster (the cluster is in normal mode), add a machine-machine user. Bind the user to the created role.

   c. Change the initial password.

#. Log in to MRS Manager as a user with the **Manager_administrator** and **Manager_viewer** permissions and choose **Cluster** > **SQL Inspector**.

#. .. _admin_guide_000427__li7650134142117:

   Add a rule for Doris by referring to :ref:`Adding an SQL Inspection <admin_guide_000409>`.

   For details about the rules supported by the Doris SQL engine, see :ref:`MRS SQL Inspection Rules <admin_guide_000409__en-us_topic_0000001662442869_section19510043143814>`.

   For example, add the **static_0001** rule while setting the threshold to **1** for the **Hint** action and **6** for the **Intercept** action. This rule detects a SQL statement that contains more than one **count distinct**.


   .. figure:: /_static/images/en-us_image_0000002379936846.png
      :alt: **Figure 2** Adding a Doris SQL inspection rule

      **Figure 2** Adding a Doris SQL inspection rule

#. Log in to the node where MySQL is installed and connect to the Doris database.

   If Kerberos authentication (security mode) has been enabled for the cluster, run the following commands to connect to the Doris database:

   **export LIBMYSQL_ENABLE_CLEARTEXT_PLUGIN=1**

   -  Directly connect to the FE node to access the Doris database.

      **mysql -u**\ *Database login username* **-p** **-P**\ *Connection port for FE queries* **-h**\ *IP address of the Doris FE instance*

      Enter the password for logging in to the database.

   -  Connect the DBalancer service. DBalancer connects to the FE node to access the Doris database based on the configured policy.

      **mysql -u**\ *Database login user* **-p** **-P**\ *TCP access port of DBalancer* **-h**\ *IP address of the Doris DBalancer instance*

      Enter the password for logging in to the database.

   .. note::

      -  The database login user is the user created in :ref:`1 <admin_guide_000427__li141114717911>` and has the Doris administrator permission.
      -  To obtain the query connection port of the Doris FE instance, you can log in to MRS Manager, choose **Cluster** > **Services** > **Doris** > **Configurations**, and query the value of **query_port** of the Doris service.
      -  To obtain the query connection port of the Doris FE instance, you can log in to MRS Manager, choose **Cluster** > **Services** > **Doris** > **Configurations**, and query the value of **balancer_tcp_port** of the Doris service.
      -  To obtain the IP address of the Doris FE or DBalancer instance, log in to MRS Manager of the MRS cluster and choose **Cluster** > **Services** > **Doris** > **Instances** to view the service IP address of any FE or DBalancer instance.
      -  You can also use the MySQL connection software or Doris web UI to connect to the database.

   Enter the password of the **dorisuser** user after running the command.

#. Check the configured SQL inspection rules.

   **use \__internal_schema;**

   **select \* from sqldefend_rule;**

   .. code-block::

      +-------------+----------+--------------------+--------+-----------------+------+------+------+
      | rule_name   | is_group | group_or_user_name | action | threshold_value | p_1  | p_2  | p_3  |
      +-------------+----------+--------------------+--------+-----------------+------+------+------+
      | static_0001 |        1 | A                  |      1 |               3 | NULL | NULL | NULL |
      | static_0001 |        1 | A                  |      2 |               2 | NULL | NULL | NULL |
      +-------------+----------+--------------------+--------+-----------------+------+------+------+

#. Create a database and switch to the database.

   **create database** *test*\ **;**

   **use** *test*\ **;**

#. Create tables **t1**, **t2**, and **t3**.

   **create table if not exists** *t1*\ **(id int) engine=olap distributed by hash(id);**

   **create table if not exists** *t2*\ **(id int) engine=olap distributed by hash(id);**

   **create table if not exists** *t3*\ **(id int) engine=olap distributed by hash(id);**

#. Check whether the **static_0001** rule has taken effect.

   **select count(distinct id) from** *t1* **except select count(distinct id) from** *t2* **intersect select count(distinct id) from** *t3* **union all select count(distinct id) from** *t1* **except select count(distinct id) from** *t2* **intersect select count(distinct id) from** *t3*\ **;**

   The number of **count distinct** in this statement exceeds the threshold configured in :ref:`3 <admin_guide_000427__li7650134142117>`.

   -  If the number of **count distinct** is greater than the threshold for a hint but is no more than the threshold for interception, the statement will be executed successfully. Run the following command to view the detailed prompt information:

      **show warnings;**

      .. code-block::

         +----------------------------------------------+-------------+------------------------------------------------------------------------------------+
         | QueryId                                      | RuleType    | Message                                                                            |
         +----------------------------------------------+-------------+------------------------------------------------------------------------------------+
         | stmt[306, 887f43753bb749c9-b6ed36350f9454a8] | STATIC_RULE | static_0001 number of count(distinct) in the query 6 more than the allowed limit 1 |
         +----------------------------------------------+-------------+------------------------------------------------------------------------------------+

      *887f43753bb749c9-b6ed36350f9454a8* indicates the query ID. To view the SQL statement corresponding to the message, run the following command:

      **select \* from query_history where query_id='**\ *887f43753bb749c9-b6ed36350f9454a8*\ **';**

   -  If number of **count distinct** is greater than the interception threshold, the statement will be interrupted and fail to be executed and the following information is displayed:

      .. code-block::

         ERROR ... detailMessage = static_0001 number of count(distinct) in the query 7 more than the allowed limit 6

      **show warnings;**

      The statement output is empty.

      .. code-block::

         Empty set (0.00 sec)

   .. note::

      -  If the action set in the SQL inspection rule is **Block**, the following information may be displayed:

         .. code-block::

            ERROR ... detailMessage = running_0001 Num of result rows num reaches the fuse threshold(1000), so cancel the output

      -  You can query SQL inspection details in **/var/log/Bigdata/doris/fe/fe.log** and **/var/log/Bigdata/audit/doris/fe/fe.audit.log**.
