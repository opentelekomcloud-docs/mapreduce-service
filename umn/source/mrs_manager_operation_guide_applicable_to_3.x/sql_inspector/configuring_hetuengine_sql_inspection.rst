:original_name: admin_guide_000416.html

.. _admin_guide_000416:

Configuring HetuEngine SQL Inspection
=====================================

Scenario
--------

You can configure rules for HetuEngine SQL inspection on FusionInsight Manager and configure rule parameters as you need.

Prerequisites
-------------

-  The cluster client that contains the HetuEngine service has been installed in the **/opt/hadoopclient** directory.
-  The HetuEngine service and compute instances are running properly.
-  If Kerberos authentication has been enabled for the cluster, you need to create a HetuEngine user and grant related permissions to the user. In addition, you need to use Ranger to assign the user the permission to manage databases, tables, and columns of the data source.

Constraints
-----------

-  The default dynamic validity period of a rule is 5 minutes.
-  Interception and blocking rules will interrupt SQL queries, so you need to set parameters of these rules properly based on the site requirements.
-  Blocking rules are controlled by session-level parameters of the system. To configure blocking rules, service users must have the set session permission.
-  For static rule **static_0003**, the total number of joins in queries does not include Semi joins and Anti joins.
-  When prompt rules are configured for dynamic_0001 and dynamic_0002, prompt messages are recorded only in logs and are not displayed on the client.
-  The client and server send asynchronous requests. For blocking rule **Running_0001**, after the server blocks the requests, the message "Query is gone " may be displayed on the client. In this case, you can view logs to check whether the requests are blocked.

Procedure
---------

#. Log in to FusionInsight Manager, click **Cluster**, and choose **SQL Inspector**. The **SQL Inspector** page is displayed.

#. .. _admin_guide_000416__en-us_topic_0000001625941690_li7650134142117:

   Add rules for HetuEngine by referring to :ref:`Adding an SQL Inspection <admin_guide_000409>`.

   For details about the rules supported by the HetuEngine SQL engine, see :ref:`MRS SQL Inspection Rules <admin_guide_000409__en-us_topic_0000001662442869_section19510043143814>`.

   For example, add a rule whose ID is **static_0001** to check whether count distinct appears more than two times in the SQL statement. If so, the system displays a hint.


   .. figure:: /_static/images/en-us_image_0000002007758273.png
      :alt: **Figure 1** Adding a HetuEngine SQL inspection rule

      **Figure 1** Adding a HetuEngine SQL inspection rule

#. Log in to the node where the HetuEngine client is installed and run the following command to switch to the client installation directory:

   **cd /opt/hadoopclient**

   Run the following command to set environment variables:

   **source bigdata_env**

#. Log in to the HetuEngine client based on the cluster authentication mode.

   -  In security mode, run the following command to authenticate the user and log in to the HetuEngine client:

      **kinit hetu_test**

      **hetu-cli --catalog hive --tenant default --schema default**

   -  In normal mode, run the following command to log in to the HetuEngine client:

      **hetu-cli --catalog hive --tenant default --schema default --user hetu_test**

      .. note::

         **hetu_test** is a service user who has at least the tenant role specified by **--tenant** and cannot be an OS user.

#. Check whether the current rule takes effect.

   Run the following statement to create a table:

   **CREATE TABLE table1(id int, name varchar,rank int);**

   **INSERT INTO table1 VALUES(10,'sachin',1),(45,'rohit',2),(46,'rohit',3),(18,'virat',4),(25,'dhawan',5);**

   Run the following statement to query data:

   **select count(distinct id),count(distinct id),count(distinct id),count(distinct id),count(distinct id),count(distinct id) from table1;**

   If the number of times count distinct appears in the statement exceeds the threshold configured in :ref:`2 <admin_guide_000416__en-us_topic_0000001625941690_li7650134142117>`, the following information is displayed:

   .. code-block::

      WARNING: Occurrence number of 'COUNT(DISTINCT XX)' (6) reaches the hint limitation (2)

   .. note::

      -  If the action set in the rule is **Intercept** or **Block**, the following information may be displayed:

         .. code-block::

            Intercepted. Reason: Occurrence number of 'COUNT(DISTINCT XX)' (6) reaches the interception limitation (2)

      -  You can query HetuEngine SQL inspection details in logs stored in **hdfs://hacluster/hetuserverhistory/tenant/coordinator/application_ID/container_ID/yyyyMMdd/server.log**.

      -  If warning information is required for JDBC secondary development, add the following configuration for the JDBC application:

         .. code-block::

            statement = connection.prepareStatement(sql.trim());
            resultSet = statement.executeQuery();
            SQLWarning sqlWarning = statement.getWarnings();
