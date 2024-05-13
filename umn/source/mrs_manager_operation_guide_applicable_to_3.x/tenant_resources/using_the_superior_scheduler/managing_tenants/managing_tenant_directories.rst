:original_name: admin_guide_000105.html

.. _admin_guide_000105:

Managing Tenant Directories
===========================

Scenario
--------

You can manage the HDFS storage directories used by specified tenants based on service requirements on MRS Manager, such as adding tenant directories, changing the quotas for directories and files and for storage space, and deleting directories.

Prerequisites
-------------

A tenant with HDFS storage resources has been added.

Viewing a Tenant Directory
--------------------------

#. Log in to MRS Manager and choose **Tenant Resources**.
#. In the tenant list on the left, click the target tenant.
#. Click the **Resource** tab.
#. View the **HDFS Storage** table.

   -  The **File Number Threshold** column provides the quota for files and directories of the tenant directory.
   -  The **Space Quota** column provides the storage space size of the tenant directory.

Adding a Tenant Directory
-------------------------

#. On MRS Manager, choose **Tenant Resources**.
#. In the tenant list on the left, click the target tenant.
#. Click the **Resource** tab.
#. In the **HDFS Storage** area, click **Create Directory**.

   -  **Parent Directory**: indicates the storage directory used by the parent tenant of the current tenant.

      .. note::

         This parameter is not displayed if the current tenant is not a sub-tenant.

   -  Set **Path** to a tenant directory path.

      .. note::

         If the current tenant is not a sub-tenant, the new path is created in the HDFS root directory.

   -  Set **Quota** to the quota for files and directories.
   -  **File Number Threshold (%)** is valid only when **Quota** is set. If the ratio of the number of used files to the value of **Quota** exceeds the value of this parameter, an alarm is generated. If this parameter is not specified, no alarm is reported in this scenario.

      .. note::

         The number of used files is collected every hour. Therefore, the alarm indicating that the ratio of used files exceeds the threshold is delayed.

   -  Set **Space Quota** to the storage space size of the tenant directory.
   -  If the ratio of used storage space to the value of **Space Quota** exceeds the **Storage Space Threshold (%)** value, an alarm is generated. If this parameter is not specified, no alarm is reported in this scenario.

      .. note::

         The used storage space is collected every hour. Therefore, the alarm indicating that the ratio of used storage space exceeds the threshold is delayed.

#. Click **OK**.

Modifying a Tenant Directory
----------------------------

#. On MRS Manager, choose **Tenant Resources**.
#. In the tenant list on the left, click the target tenant.
#. Click the **Resource** tab.
#. In the **HDFS Storage** table, click **Modify** in the **Operation** column of the specified tenant directory.

   -  Set **Quota** to the quota for files and directories.
   -  **File Number Threshold (%)** is valid only when **Quota** is set. If the ratio of the number of used files to the value of **Quota** exceeds the value of this parameter, an alarm is generated. If this parameter is not specified, no alarm is reported in this scenario.
   -  Set **Space Quota** to the storage space size of the tenant directory.
   -  If the ratio of used storage space to the value of **Space Quota** exceeds the **Storage Space Threshold (%)** value, an alarm is generated. If this parameter is not specified, no alarm is reported in this scenario.

#. Click **OK**.

Deleting a Tenant Directory
---------------------------

#. On MRS Manager, choose **Tenant Resources**.
#. In the tenant list on the left, click the target tenant.
#. Click the **Resource** tab.
#. In the **HDFS Storage** table, click **Delete** in the **Operation** column of the specified tenant directory.

   .. note::

      The tenant directory that is created by the system during tenant creation cannot be deleted.

#. Click **OK**.
