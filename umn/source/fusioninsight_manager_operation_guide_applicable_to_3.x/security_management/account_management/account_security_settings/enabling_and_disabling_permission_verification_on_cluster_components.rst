:original_name: admin_guide_000247.html

.. _admin_guide_000247:

Enabling and Disabling Permission Verification on Cluster Components
====================================================================

Scenario
--------

HDFS and ZooKeeper verify the permission of users who attempt to access the services in both security and normal clusters by default. Users without related permission cannot access resources in HDFS and ZooKeeper. When the cluster is deployed in normal mode, HBase and YARN do not verify the permission of users who attempt to access the services by default. All users can access resources in HBase and YARN.

Based on actual service requirements, administrators can enable permission verification on HBase and YARN or disable permission verification on HDFS and ZooKeeper in normal clusters.

Impact on the System
--------------------

After the enabling and disabling operations, the service configuration will expire. You need to restart the corresponding service for the configuration to take effect.

Enabling Permission Verification on HBase
-----------------------------------------

#. Log in to FusionInsight Manager.

#. Click **Cluster**, click the name of the desired cluster, choose **Services** > **Ranger**, and click **Configurations**.

#. Click **All Configurations**.

#. Search for parameters **hbase.coprocessor.region.classes**, **hbase.coprocessor.master.classes**, and **hbase.coprocessor.regionserver.classes**.

   Add the coprocessor parameter **org.apache.hadoop.hbase.security.access.AccessController** to the end of the values of the preceding parameters, and use a comma (,) to separate the values from those of the original coprocessors.

#. Click **Save**, click **OK**, and wait for message "Operation successful" to display.

Disabling Permission Verification on HBase
------------------------------------------

.. note::

   After HBase permission verification is disabled, the existing permission data will be retained. If you want to delete permission information, disable permission verification, enter the HBase shell, and delete table **hbase:acl**.

#. Log in to FusionInsight Manager.

#. Click **Cluster**, click the name of the desired cluster, choose **Services** > **HBase**, and click **Configurations**.

#. Click **All Configurations**.

#. Search for parameters **hbase.coprocessor.region.classes**, **hbase.coprocessor.master.classes**, and **hbase.coprocessor.regionserver.classes**.

   Delete the coprocessor parameter **org.apache.hadoop.hbase.security.access.AccessController**.

#. Click **Save**, click **OK**, and wait for message "Operation successful" to display.

Disabling Permission Verification on HDFS
-----------------------------------------

#. Log in to FusionInsight Manager.
#. Click **Cluster**, click the name of the desired cluster, choose **Services** > **HDFS**, and click **Configurations**.
#. Click **All Configurations**.
#. Search for parameters **dfs.namenode.acls.enabled** and **dfs.permissions.enabled**.

   -  **dfs.namenode.acls.enabled** indicates whether to enable HDFS ACL. The default value is **true**, indicating that the ACL is enabled. Change the value to **false**.
   -  **dfs.permissions.enabled** indicates whether to enable permission check for HDFS. The default value is **true**, indicating that permission check is enabled. Change the value to **false**. After the modification, the owner, owner group, and permission of the directories and files in HDFS remain unchanged.

#. Click **Save**, click **OK**, and wait for message "Operation successful" to display.

Enabling Permission Verification on YARN
----------------------------------------

#. Log in to FusionInsight Manager.

#. Click **Cluster**, click the name of the desired cluster, choose **Services** > **Yarn**, and click **Configurations**.

#. Click **All Configurations**.

#. Search for parameter **yarn.acl.enable**.

   **yarn.acl.enable** indicates whether to enable the permission check for YARN.

   -  In normal clusters, the value is set to **false** by default to disable permission check. To enable permission check, change the value to **true**.
   -  In security clusters, the value is set to **true** by default to enable authentication.

#. Click **Save**, click **OK**, and wait for message "Operation successful" to display.

Disabling Permission Verification on ZooKeeper
----------------------------------------------

#. Log in to FusionInsight Manager.

#. Click **Cluster**, click the name of the desired cluster, choose **Services** > **ZooKeeper**, and click **Configurations**.

#. Click **All Configurations**.

#. Search for parameter **skipACL**.

   **skipACL** indicates whether to skip the ZooKeeper permission check. The default value is **no**, indicating that permission check is enabled. Change the value to **yes**.

#. Click **Save**, click **OK**, and wait for message "Operation successful" to display.
