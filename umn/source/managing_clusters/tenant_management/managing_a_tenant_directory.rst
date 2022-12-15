:original_name: mrs_01_0308.html

.. _mrs_01_0308:

Managing a Tenant Directory
===========================

Scenario
--------

You can manage the HDFS storage directory used by a specific tenant on MRS. The management operations include adding a tenant directory, modifying the directory file quota, modifying the storage space, and deleting a directory.

Prerequisites
-------------

-  A tenant associated with HDFS storage resources has been added.
-  You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

-  View a tenant directory.

   #. On the MRS details page, click **Tenants**.

      .. note::

         For MRS 1.7.2 or earlier, see :ref:`Managing a Tenant Directory <mrs_01_0542>`. For MRS 3.x or later, see :ref:`Overview <admin_guide_000097>`.

   #. In the tenant list on the left, click the target tenant.
   #. Click the **Resources** tab.
   #. View the **HDFS Storage** table.

      -  The **Maximum Number of Files/Directories** column indicates the quotas for the file and directory quantity of the tenant directory.
      -  The **Space Quota** column indicates storage space size of tenant directories.

-  Add a tenant directory.

   #. On the MRS details page, click **Tenants**.

      .. note::

         For MRS 1.7.2 or earlier, see :ref:`Managing a Tenant Directory <mrs_01_0542>`. For MRS 3.x or later, see :ref:`Overview <admin_guide_000097>`.

   #. In the tenant list on the left, click the tenant whose HDFS storage directory needs to be added.
   #. Click the **Resources** tab.
   #. In the **HDFS Storage** table, click **Create Directory**.

      -  Set **Path** to a tenant directory path.

         .. note::

            -  If the current tenant is not a sub-tenant, the new path is created in the HDFS root directory.
            -  If the current tenant is a sub-tenant, the new path is created in the specified directory.

         A complete HDFS storage directory can contain a maximum of 1,023 characters. An HDFS directory name contains digits, letters, spaces, and underscores (_). The name cannot start or end with a space.

      -  Set **Maximum Number of Files/Directories** to the quotas of file and directory quantity.

         **Maximum Number of Files/Directories** is optional. Its value ranges from **1** to **9223372036854775806**.

      -  Set **Storage Space Quota** to the storage space size of the tenant directory.

         The value of **Storage Space Quota** ranges from **1** to **8796093022208**.

         .. note::

            To ensure data reliability, one backup is automatically generated for each file saved in HDFS, that is, two copies are generated in total. The HDFS storage space indicates the total disk space occupied by all these copies. For example, if the value of **Storage Space Quota** is set to **500**, the actual space for storing files is about 250 MB (500/2 = 250).

   #. Click **OK**. The system creates tenant directories in the HDFS root directory.

-  Modify a tenant directory.

   #. On the MRS details page, click **Tenants**.

      .. note::

         For MRS 1.7.2 or earlier, see :ref:`Managing a Tenant Directory <mrs_01_0542>`. For MRS 3.x or later, see :ref:`Overview <admin_guide_000097>`.

   #. In the tenant list on the left, click the tenant whose HDFS storage directory needs to be modified.
   #. Click the **Resources** tab.
   #. In the **HDFS Storage** table, click **Modify** in the **Operation** column of the specified tenant directory.

      -  Set **Maximum Number of Files/Directories** to the quotas of file and directory quantity.

         **Maximum Number of Files/Directories** is optional. Its value ranges from **1** to **9223372036854775806**.

      -  Set **Storage Space Quota** to the storage space size of the tenant directory.

         The value of **Storage Space Quota** ranges from **1** to **8796093022208**.

         .. note::

            To ensure data reliability, one backup is automatically generated for each file saved in HDFS, that is, two copies are generated in total. The HDFS storage space indicates the total disk space occupied by all these copies. For example, if the value of **Storage Space Quota** is set to **500**, the actual space for storing files is about 250 MB (500/2 = 250).

   #. Click **OK**.

-  Delete a tenant directory.

   #. On the MRS details page, click **Tenants**.

      .. note::

         For MRS 1.7.2 or earlier, see :ref:`Managing a Tenant Directory <mrs_01_0542>`. For MRS 3.x or later, see :ref:`Overview <admin_guide_000097>`.

   #. In the tenant list on the left, click the tenant whose HDFS storage directory needs to be deleted.

   #. Click the **Resources** tab.

   #. In the **HDFS Storage** table, click **Delete** in the **Operation** column of the specified tenant directory.

      The default HDFS storage directory set during tenant creation cannot be deleted. Only the newly added HDFS storage directory can be deleted.

   #. Click **OK**. The tenant directory is deleted.
