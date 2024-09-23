:original_name: admin_guide_000412.html

.. _admin_guide_000412:

Configuring Hive SQL Inspection
===============================

Scenario
--------

You can configure rules for Hive SQL inspection on FusionInsight Manager and configure rule parameters as you need.

Prerequisites
-------------

-  The cluster client that contains the Hive service has been installed in the **/opt/hadoopclient** directory.
-  The Hive service of the cluster is running properly.
-  For a cluster with Kerberos authentication enabled, a user with Hive operation permissions has been created.

Constraints
-----------

-  By default, SQL inspection rules need 5 seconds to take effect dynamically. After the queue is modified, it takes 10 minutes for Hive inspection rules to be reloaded.
-  Interception and blocking rules will interrupt SQL tasks, so you need to set parameters of these rules properly based on the site requirements.
-  For the rule dynamic_0001 (the number of files scanned by SQL statements exceeds the threshold), when the Spark and Tez engines reach the threshold, interception logs are printed in Yarn task logs and cannot be output on the Beeline client.
-  Blocking rules have execution latency. For example, if the running_0004 rule is used and the threshold of the scanned data volume is 10 GB, the statement may be blocked when the data volume is 15 GB or higher due to the determination period and task concurrency.

Procedure
---------

#. Log in to FusionInsight Manager, click **Cluster**, and choose **SQL Inspector**. The **SQL Inspector** page is displayed.

#. .. _admin_guide_000412__en-us_topic_0000001662482833_li7650134142117:

   Add rules for Hive by referring to :ref:`Adding an SQL Inspection <admin_guide_000409>`.

   For details about the rules supported by the Hive SQL engine, see :ref:`MRS SQL Inspection Rules <admin_guide_000409__en-us_topic_0000001662442869_section19510043143814>`.

   For example, add a rule whose ID is **static_0001** to check whether count distinct appears more than two times in the SQL statement. If so, the system displays a hint.


   .. figure:: /_static/images/en-us_image_0000001971237698.png
      :alt: **Figure 1** Adding a Hive SQL inspection rule

      **Figure 1** Adding a Hive SQL inspection rule

#. Log in to the node where the Hive client is installed and run the following command to switch to the client installation directory.

   **cd /opt/hadoopclient**

   Run the following command to set environment variables:

   **source bigdata_env**

   Run the following command to authenticate the current user. Skip this step if Kerberos authentication is disabled for the cluster (the cluster is in normal mode).

   **kinit** *Component service user who has the Hive operation permission*

#. Run the following command to log in to the Hive client:

   **beeline**

#. Run the following commands to create a table and import data to the table.

   **drop table if exists hivetb;**

   **create table hivetb(a int,b int);**

   **insert into hivetb select 1,11;**

   **insert into hivetb select 2,22;**

#. Run the following SQL statement to check whether the current rule takes effect:

   **select count(distinct a),count(distinct b) from hivetb;**

   If the number of times count distinct appears in the statement exceeds the threshold configured in :ref:`2 <admin_guide_000412__en-us_topic_0000001662482833_li7650134142117>`, the following information is displayed:

   .. code-block::

      ...
      WARN  : STATIC_0001 The count(distinct X) times exceeds the limit : 2, current count distinct times : 2
      ...

   If the operation set in the rule is **Block**, the statement fails to be executed and the following information is displayed:

   .. code-block::

      ...
      Error: Error while compiling statement: FAILED: RuleException STATIC_0001 The count(distinct X) times exceeds the limit : 2, current count distinct times : 2 (state=42000,code=40000)
      ...

   .. note::

      -  For more Hive SQL inspection rules, see :ref:`MRS SQL Inspection Rules <admin_guide_000409__en-us_topic_0000001662442869_section19510043143814>`.
      -  You can also obtain the SQL inspection rules via logs which are stored in **/var/log/Bigdata/audit/hive/hiveserver/queryinfo.log**.
