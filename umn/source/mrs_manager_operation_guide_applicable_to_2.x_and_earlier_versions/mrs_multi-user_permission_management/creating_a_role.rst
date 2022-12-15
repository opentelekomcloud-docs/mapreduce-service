:original_name: mrs_01_0343.html

.. _mrs_01_0343:

Creating a Role
===============

Scenario
--------

This section describes how to create a role on Manager and authorize and manage Manager and components.

Up to 1000 roles can be created on Manager.

.. note::

   The operations described in this section apply only to clusters of versions earlier than MRS 3.x.

   For clusters of **MRS 3.\ x** or later, see :ref:`Managing Roles <admin_guide_000148>`.

Prerequisites
-------------

-  You have learned service requirements.
-  You have obtained a cluster with Kerberos authentication enabled or a common cluster with the EIP function enabled.

Procedure
---------

#. Access MRS Manager. For details, see :ref:`Accessing MRS Manager MRS 2.1.0 or Earlier) <mrs_01_0102>`.

#. On MRS Manager, choose **System** > **Manage Role**.

#. Click **Create Role** and fill in **Role Name** and **Description**.

   **Role Name** is mandatory and contains 3 to 30 characters. Only digits, letters, and underscores (_) are allowed. **Description** is optional.

#. In **Permission**, set role permission.

   a. Click **Service Name** and select a name in **View Name**.
   b. Select one or more permissions.

   .. note::

      -  The **Permission** parameter is optional.
      -  If you select **View Name** to set component permissions, you can enter a resource name in the **Search** box in the upper right corner and click |image1|. The search result is displayed.
      -  The search scope covers only directories with current permissions. You cannot search subdirectories. Search by keywords supports fuzzy match and is case-insensitive. Results of the next page can be searched.

   .. table:: **Table 1** Manager permission description

      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
      | Resource Supporting Permission Management | Permission Setting                                                                                                                     |
      +===========================================+========================================================================================================================================+
      | **Alarm**                                 | Authorizes the Manager alarm function. You can select **View** to view alarms and **Management** to manage alarms.                     |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
      | **Audit**                                 | Authorizes the Manager audit log function. You can select **View** to view audit logs and **Management** to manage audit logs.         |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
      | **Dashboard**                             | Authorizes the Manager overview function. You can select **View** to view the cluster overview.                                        |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
      | **Hosts**                                 | Authorizes the node management function. You can select **View** to view node information and **Management** to manage nodes.          |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
      | **Services**                              | Authorizes the service management function. You can select **View** to view service information and **Management** to manage services. |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
      | **System_cluster_management**             | Authorizes the MRS cluster management function. You can select **Management** to use the MRS patch management function.                |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
      | **System_configuration**                  | Authorizes the MRS cluster configuration function. You can select **Management** to configure MRS clusters on Manager.                 |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
      | **System_task**                           | Authorizes the MRS cluster task function. You can select **Management** to manage periodic tasks of MRS clusters on Manager.           |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+
      | **Tenant**                                | Authorizes the Manager multi-tenant management function. You can select **Management** to manage multi-tenants.                        |
      +-------------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------+

   .. table:: **Table 2** HBase permission description

      +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
      | Resource Supporting Permission Management | Permission Setting                                                                                                |
      +===========================================+===================================================================================================================+
      | **SUPER_USER_GROUP**                      | Grants you HBase administrator permissions.                                                                       |
      +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
      | **Global**                                | HBase resource type, indicating the whole HBase.                                                                  |
      +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
      | **Namespace**                             | HBase resource type, indicating namespace, which is used to store HBase tables. It has the following permissions: |
      |                                           |                                                                                                                   |
      |                                           | -  **Admin** permission to manage the namespace                                                                   |
      |                                           | -  **Create**: permission to create HBase tables in the namespace                                                 |
      |                                           | -  **Read**: permission to access the namespace                                                                   |
      |                                           | -  **Write**: permission to write data to the namespace                                                           |
      |                                           | -  **Execute**: permission to execute the coprocessor (Endpoint)                                                  |
      +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
      | **Table**                                 | HBase resource type, indicating a data table, which is used to store data. It has the following permissions:      |
      |                                           |                                                                                                                   |
      |                                           | -  **Admin**: permission to manage a data table                                                                   |
      |                                           | -  **Create**: permission to create column families and columns in a data table                                   |
      |                                           | -  **Read**: permission to read a data table                                                                      |
      |                                           | -  **Write**: permission to write data to a data table                                                            |
      |                                           | -  **Execute**: permission to execute the coprocessor (Endpoint)                                                  |
      +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
      | **ColumnFamily**                          | HBase resource type, indicating a column family, which is used to store data. It has the following permissions:   |
      |                                           |                                                                                                                   |
      |                                           | -  **Create**: permission to create columns in a column family                                                    |
      |                                           | -  **Read**: permission to read a column family                                                                   |
      |                                           | -  **Write**: permission to write data to a column family                                                         |
      +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------+
      | **Qualifier**                             | HBase resource type, indicating a column, which is used to store data. It has the following permissions:          |
      |                                           |                                                                                                                   |
      |                                           | -  **Read**: permission to read a column                                                                          |
      |                                           | -  **Write**: permission to write data to a column                                                                |
      +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------+

   By default, permissions of an HBase resource type of each level are shared by resource types of sub-levels. However, the **Recursive** option is not selected by default. For example, if **Read** and **Write** permissions are added to the **default** namespace, they are automatically added to the tables, column families, and columns in the namespace. If a child resource is set after the parent resource, the permission of the child resource is the union of the permissions of the parent resource and the current child resource.

   .. table:: **Table 3** HDFS permission description

      +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
      | Resource Supporting Permission Management | Permission Setting                                                                                                                  |
      +===========================================+=====================================================================================================================================+
      | **Folder**                                | HDFS resource type, indicating an HDFS directory, which is used to store files or subdirectories. It has the following permissions: |
      |                                           |                                                                                                                                     |
      |                                           | -  **Read**: permission to access the HDFS directory                                                                                |
      |                                           | -  **Write**: permission to write data to the HDFS directory                                                                        |
      |                                           | -  **Execute**: permission to perform an operation. It must be selected when you add access or write permission.                    |
      +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+
      | **Files**                                 | HDFS resource type, indicating a file in HDFS. It has the following permissions:                                                    |
      |                                           |                                                                                                                                     |
      |                                           | -  **Read**: permission to access the file                                                                                          |
      |                                           | -  **Write**: permission to write data to the file                                                                                  |
      |                                           | -  **Execute**: permission to perform an operation. It must be selected when you add access or write permission.                    |
      +-------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------+

   Permissions of an HDFS directory of each level are not shared by directory types of sub-levels by default. For example, if **Read** and **Execute** permissions are added to the **tmp** directory, you must select **Recursive** for permissions to be added to subdirectories.

   .. table:: **Table 4** Hive permission description

      +-------------------------------------------+-----------------------------------------------------------------------------------------------------------------------+
      | Resource Supporting Permission Management | Permission Setting                                                                                                    |
      +===========================================+=======================================================================================================================+
      | **Hive Admin Privilege**                  | Grants you Hive administrator permissions.                                                                            |
      +-------------------------------------------+-----------------------------------------------------------------------------------------------------------------------+
      | **Database**                              | Hive resource type, indicating a Hive database, which is used to store Hive tables. It has the following permissions: |
      |                                           |                                                                                                                       |
      |                                           | -  **Select**: permission to query the Hive database                                                                  |
      |                                           | -  **Delete**: permission to perform the deletion operation in the Hive database                                      |
      |                                           | -  **Insert**: permission to perform the insertion operation in the Hive database                                     |
      |                                           | -  **Create**: permission to perform the creation operation in the Hive database                                      |
      +-------------------------------------------+-----------------------------------------------------------------------------------------------------------------------+
      | **Table**                                 | Hive resource type, indicating a Hive table, which is used to store data. It has the following permissions:           |
      |                                           |                                                                                                                       |
      |                                           | -  **Select**: permission to query the Hive table                                                                     |
      |                                           | -  **Delete**: permission to perform the deletion operation in the Hive table                                         |
      |                                           | -  **Update**: permission to perform the update operation in the Hive table                                           |
      |                                           | -  **Insert**: permission to perform the insertion operation in the Hive table                                        |
      |                                           | -  **Grant of Select**: permission to grant the **Select** permission to other users using Hive statements            |
      |                                           | -  **Grant of Delete**: permission to grant the **Delete** permission to other users using Hive statements            |
      |                                           | -  **Grant of Update**: permission to grant the **Update** permission to other users using Hive statements            |
      |                                           | -  **Grant of Insert**: permission to grant the **Insert** permission to other users using Hive statements            |
      +-------------------------------------------+-----------------------------------------------------------------------------------------------------------------------+

   By default, permissions of a Hive resource type of each level are shared by resource types of sub-levels. However, the **Recursive** option is not selected by default. For example, if **Select** and **Insert** permissions are added to the **default** database, they are automatically added to the tables and columns in the database. If a child resource is set after the parent resource, the permission of the child resource is the union of the permissions of the parent resource and the current child resource.

   .. table:: **Table 5** Yarn permission description

      +-------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | Resource Supporting Permission Management | Permission Setting                                                                                                                               |
      +===========================================+==================================================================================================================================================+
      | **Cluster Admin Operations**              | Grants you Yarn administrator permissions.                                                                                                       |
      +-------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | **root**                                  | Root queue of Yarn. It has the following permissions:                                                                                            |
      |                                           |                                                                                                                                                  |
      |                                           | -  **Submit**: permission to submit jobs in the queue                                                                                            |
      |                                           | -  **Admin**: permission to manage permissions of the current queue                                                                              |
      +-------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | **Parent Queue**                          | Yarn resource type, indicating a parent queue containing sub-queues. A root queue is a type of a parent queue. It has the following permissions: |
      |                                           |                                                                                                                                                  |
      |                                           | -  **Submit**: permission to submit jobs in the queue                                                                                            |
      |                                           | -  **Admin**: permission to manage permissions of the current queue                                                                              |
      +-------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
      | **Leaf Queue**                            | Yarn resource type, indicating a leaf queue. It has the following permissions:                                                                   |
      |                                           |                                                                                                                                                  |
      |                                           | -  **Submit**: permission to submit jobs in the queue                                                                                            |
      |                                           | -  **Admin**: permission to manage permissions of the current queue                                                                              |
      +-------------------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------+

   By default, permissions of a Yarn resource type of each level are shared by resource types of sub-levels. However, the **Recursive** option is not selected by default. For example, if the **Submit** permission is added to the **root** queue, it is automatically added to the sub-queue. Permissions inherited by sub-queues will not be displayed as selected in the **Permission** table. If a child resource is set after the parent resource, the permission of the child resource is the union of the permissions of the parent resource and the current child resource.

   .. table:: **Table 6** Hue permission description

      +-------------------------------------------+------------------------------------------------------+
      | Resource Supporting Permission Management | Permission Setting                                   |
      +===========================================+======================================================+
      | **Storage Policy Admin**                  | Grants you storage policy administrator permissions. |
      +-------------------------------------------+------------------------------------------------------+

#. Click **OK**. Return to **Manage Role**.

Related Tasks
-------------

**Modifying a role**

#. On MRS Manager, click **System**.
#. In the **Permission** area, click **Manage Role**.
#. In the row of the role to be modified, click **Modify** to modify role information.

   .. note::

      If you modify permissions assigned by the role, it takes 3 minutes to make new configurations take effect.

#. Click **OK**. The modification is complete.

**Deleting a role**

#. On MRS Manager, click **System**.
#. In the **Permission** area, click **Manage Role**.
#. In the row of the role to be deleted, click **Delete**.
#. Click **OK**. The role is deleted.

.. |image1| image:: /_static/images/en-us_image_0000001349057965.png
