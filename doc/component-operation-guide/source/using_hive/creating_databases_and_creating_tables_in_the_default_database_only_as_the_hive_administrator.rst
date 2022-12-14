:original_name: mrs_01_0969.html

.. _mrs_01_0969:

Creating Databases and Creating Tables in the Default Database Only as the Hive Administrator
=============================================================================================

Scenario
--------

This function is applicable to Hive and Spark2x for MRS 3.\ *x* or later, or Hive and Spark for versions earlier than MRS 3.x.

After this function is enabled, only the Hive administrator can create databases and tables in the default database. Other users can use the databases only after being authorized by the Hive administrator.

.. note::

   -  After this function is enabled, common users are not allowed to create a database or create a table in the default database. Based on the actual application scenario, determine whether to enable this function.
   -  Permissions of common users are restricted. In the scenario where common users have been used to perform operations, such as database creation, table script migration, and metadata recreation in an earlier version of database, the users can perform such operations on the database in the condition that this function is disabled temporarily after the database is migrated or after the cluster is upgraded.

Procedure
---------

#. The Hive service configuration page is displayed.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager, choose **Services** > **Hive** > **Service Configuration**, and select **All** from the **Basic** drop-down list.
   -  For MRS 1.9.2 or later, click the cluster name on the MRS console, choose **Components** > **Hive** > **Service Configuration**, and select **All** from the **Basic** drop-down list.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

   -  For MRS 3.\ *x* or later, log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. And choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Configurations** > **All Configurations**.

#. Choose **HiveServer(Role)** > **Customization**, add a customized parameter to the **hive-site.xml** parameter file, set **Name** to **hive.allow.only.admin.create**, and set **Value** to **true**. Restart all Hive instances after the modification.
#. Determine whether to enable this function on the Spark/Spark2x client.

   -  If yes, go to :ref:`4 <mrs_01_0969__li475373212497>`.
   -  If no, no further action is required.

4. .. _mrs_01_0969__li475373212497:

   Choose **SparkResource2x** > **Customization**, add a customized parameter to the **hive-site.xml** parameter file, set **Name** to **hive.allow.only.admin.create**, and set **Value** to **true**. Then, choose **JDBCServer2x** > **Customization** and repeat the preceding operations to add the customized parameter. Restart all Spark2x instances after the modification.

5. Download and install the Spark/Spark2x client again.
