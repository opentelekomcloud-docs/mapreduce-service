:original_name: mrs_01_0542.html

.. _mrs_01_0542:

Managing a Tenant Directory
===========================

Scenario
--------

You can manage the HDFS storage directory used by a specific tenant on MRS Manager. The management operations include adding a tenant directory, modifying the directory file quota, modifying the storage space, and deleting a directory.

Prerequisites
-------------

A tenant associated with HDFS storage resources has been added.

Procedure
---------

-  Viewing a tenant directory

   #. On MRS Manager, click **Tenant**.
   #. In the tenant list on the left, click the target tenant.
   #. Click the **Resource** tab.
   #. View the **HDFS Storage** table.

      -  The Quota column indicates the quantity quotas of files and directories.
      -  The **Storage Space Quota** column indicates the storage space size of the tenant directory.

-  Adding a tenant directory

   #. On MRS Manager, click **Tenant**.
   #. In the tenant list on the left, click the tenant whose HDFS storage directory needs to be added.
   #. Click the **Resource** tab.
   #. In the **HDFS Storage** table, click **Create Directory**.

      -  In **Parent Directory**, select a storage directory of a parent tenant.

         This parameter applies only to sub-tenants. If the parent tenant has multiple directories, select any of them.

      -  Set **Path** to a tenant directory path.

         .. note::

            -  If the current tenant is not a sub-tenant, the new path is created in the HDFS root directory.
            -  If the current tenant is a sub-tenant, the new path is created in the specified directory.

         A complete HDFS storage directory can contain a maximum of 1,023 characters. An HDFS directory name contains digits, letters, spaces, and underscores (_). The name cannot start or end with a space.

      -  Set **Quota** to the quotas of file and directory quantity.

         **Maximum Number of Files/Directories** is optional. Its value ranges from **1** to **9223372036854775806**.

      -  Set **Storage Space Quota** to the storage space size of the tenant directory.

         The value of **Storage Space Quota** ranges from **1** to **8796093022208**.

         .. note::

            To ensure data reliability, one copy of a file is automatically generated when the file is stored in HDFS. That is, two copies of the same file are stored by default. The HDFS storage space indicates the total disk space occupied by all these copies. For example, if the value of **Storage Space Quota** is set to **500**, the actual space for storing files is about 250 MB (500/2 = 250).

   #. Click **OK**. The system creates tenant directories in the HDFS root directory.

-  Modify a tenant directory.

   #. On MRS Manager, click **Tenant**.
   #. In the tenant list on the left, click the tenant whose HDFS storage directory needs to be modified.
   #. Click the **Resource** tab.
   #. In the **HDFS Storage** table, click **Modify** in the **Operation** column of the specified tenant directory.

      -  Set **Quota** to the quotas of file and directory quantity.

         **Maximum Number of Files/Directories** is optional. Its value ranges from **1** to **9223372036854775806**.

      -  Set **Storage Space Quota** to the storage space size of the tenant directory.

         The value of **Storage Space Quota** ranges from **1** to **8796093022208**.

         .. note::

            To ensure data reliability, one copy of a file is automatically generated when the file is stored in HDFS. That is, two copies of the same file are stored by default. The HDFS storage space indicates the total disk space occupied by all these copies. For example, if the value of **Storage Space Quota** is set to **500**, the actual space for storing files is about 250 MB (500/2 = 250).

   #. Click **OK**.

-  Delete a tenant directory.

   #. On MRS Manager, click **Tenant**.

   #. In the tenant list on the left, click the tenant whose HDFS storage directory needs to be deleted.

   #. Click the **Resource** tab.

   #. In the **HDFS Storage** table, click **Delete** in the **Operation** column of the specified tenant directory.

      The default HDFS storage directory set during tenant creation cannot be deleted. Only the newly added HDFS storage directory can be deleted.

   #. Click **OK**.
