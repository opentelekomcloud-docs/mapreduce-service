:original_name: mrs_01_0636.html

.. _mrs_01_0636:

Configuring Presto Permissions
==============================

MRS 3.\ *x* does not enable you to configure Presto permissions.

Configuring Presto Permissions in a Security Cluster
----------------------------------------------------

By default, the Hive Catalog authorization of the Presto component is enabled in a security cluster. The Presto permission configuration procedure is as follows:

#. Log in to Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`.
#. Choose **System** > **Manage Role**, configure a role that has the Hive database/table permissions, and bind the role to the user.

Configuring Presto Permissions in a Normal Cluster
--------------------------------------------------

By default, Presto authorization is not enabled in a normal cluster. You need to manually configure Presto permissions as follows:

#. Go to the MRS cluster details page.
#. Choose **Components** > **Hive**. Set **Type** to **All**. On the displayed Hive configuration page, modify parameter settings.
#. Search for and modify the following parameters:

   -  Set **hive.security.authorization.enabled** to **true**.
   -  Set **hive.security.authorization.manager** to **org.apache.hadoop.hive.ql.security.authorization.plugin.sqlstd.SQLStdHiveAuthorizerFactory**.

#. Click **Save Configuration** and select **Restart the affected services or instances** to restart the Hive service.
#. Choose **Components** > **Presto**. Set **Type** to **All**. On the displayed Presto configuration page, modify parameter settings.
#. Search for and modify the value of **hive.security** to **sql-standard-with-group**.
#. Click **Save Configuration** and select **Restart the affected services or instances** to restart the Presto service.
#. Logging in to MRS Manager
#. Choose **System** > **Change OMS Database Password** > **Restart the OMS service**.
#. Choose **System** > **Manage Role**, configure a role that has the Hive database/table permissions, and bind the role to the user.
