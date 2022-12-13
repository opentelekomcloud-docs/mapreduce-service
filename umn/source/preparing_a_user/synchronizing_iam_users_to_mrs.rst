:original_name: mrs_01_0495.html

.. _mrs_01_0495:

Synchronizing IAM Users to MRS
==============================

IAM user synchronization is to synchronize IAM users bound with MRS policies to the MRS system and create accounts with the same usernames but different passwords as the IAM users. Then, you can use an IAM username (the password needs to be reset by user **admin** of Manager) to log in to Manager for cluster management, and submit jobs on the GUI in a cluster with Kerberos authentication enabled.

:ref:`Table 1 <mrs_01_0495__table3878619101919>` compares IAM users' permission policies and the synchronized users' permissions on MRS. For details about the default permissions on Manager, see :ref:`Users and Permissions of MRS Clusters <mrs_01_0341>`.

.. _mrs_01_0495__table3878619101919:

.. table:: **Table 1** Policy and permission mapping after synchronization

   +--------------+-----------------------------------------------------------+---------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+
   | Policy Type  | IAM Policy                                                | User's Default Permissions on MRS After Synchronization | Have Permission to Perform the Synchronization                                                                                                | Have Permission to Submit Jobs |
   +==============+===========================================================+=========================================================+===============================================================================================================================================+================================+
   | Fine-grained | MRS ReadOnlyAccess                                        | Manager_viewer                                          | No                                                                                                                                            | No                             |
   +--------------+-----------------------------------------------------------+---------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+
   |              | MRS CommonOperations                                      | -  Manager_viewer                                       | No                                                                                                                                            | Yes                            |
   |              |                                                           | -  default                                              |                                                                                                                                               |                                |
   |              |                                                           | -  launcher-job                                         |                                                                                                                                               |                                |
   +--------------+-----------------------------------------------------------+---------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+
   |              | MRS FullAccess                                            | -  Manager_administrator                                | Yes                                                                                                                                           | Yes                            |
   |              |                                                           | -  Manager_auditor                                      |                                                                                                                                               |                                |
   |              |                                                           | -  Manager_operator                                     |                                                                                                                                               |                                |
   |              |                                                           | -  Manager_tenant                                       |                                                                                                                                               |                                |
   |              |                                                           | -  Manager_viewer                                       |                                                                                                                                               |                                |
   |              |                                                           | -  System_administrator                                 |                                                                                                                                               |                                |
   |              |                                                           | -  default                                              |                                                                                                                                               |                                |
   |              |                                                           | -  launcher-job                                         |                                                                                                                                               |                                |
   +--------------+-----------------------------------------------------------+---------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+
   | RBAC         | MRS Administrator                                         | -  Manager_administrator                                | No                                                                                                                                            | Yes                            |
   |              |                                                           | -  Manager_auditor                                      |                                                                                                                                               |                                |
   |              |                                                           | -  Manager_operator                                     |                                                                                                                                               |                                |
   |              |                                                           | -  Manager_tenant                                       |                                                                                                                                               |                                |
   |              |                                                           | -  Manager_viewer                                       |                                                                                                                                               |                                |
   |              |                                                           | -  System_administrator                                 |                                                                                                                                               |                                |
   |              |                                                           | -  default                                              |                                                                                                                                               |                                |
   |              |                                                           | -  launcher-job                                         |                                                                                                                                               |                                |
   +--------------+-----------------------------------------------------------+---------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+
   |              | Server Administrator, Tenant Guest, and MRS Administrator | -  Manager_administrator                                | Yes                                                                                                                                           | Yes                            |
   |              |                                                           | -  Manager_auditor                                      |                                                                                                                                               |                                |
   |              |                                                           | -  Manager_operator                                     |                                                                                                                                               |                                |
   |              |                                                           | -  Manager_tenant                                       |                                                                                                                                               |                                |
   |              |                                                           | -  Manager_viewer                                       |                                                                                                                                               |                                |
   |              |                                                           | -  System_administrator                                 |                                                                                                                                               |                                |
   |              |                                                           | -  default                                              |                                                                                                                                               |                                |
   |              |                                                           | -  launcher-job                                         |                                                                                                                                               |                                |
   +--------------+-----------------------------------------------------------+---------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+
   |              | Tenant Administrator                                      | -  Manager_administrator                                | Yes                                                                                                                                           | Yes                            |
   |              |                                                           | -  Manager_auditor                                      |                                                                                                                                               |                                |
   |              |                                                           | -  Manager_operator                                     |                                                                                                                                               |                                |
   |              |                                                           | -  Manager_tenant                                       |                                                                                                                                               |                                |
   |              |                                                           | -  Manager_viewer                                       |                                                                                                                                               |                                |
   |              |                                                           | -  System_administrator                                 |                                                                                                                                               |                                |
   |              |                                                           | -  default                                              |                                                                                                                                               |                                |
   |              |                                                           | -  launcher-job                                         |                                                                                                                                               |                                |
   +--------------+-----------------------------------------------------------+---------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+
   | Custom       | Custom policy                                             | -  Manager_viewer                                       | -  If custom policies use RBAC policies as a template, refer to the RBAC policies.                                                            | Yes                            |
   |              |                                                           | -  default                                              | -  If custom policies use fine-grained policies as a template, refer to the fine-grained policies. The fine-grained policies are recommended. |                                |
   |              |                                                           | -  launcher-job                                         |                                                                                                                                               |                                |
   +--------------+-----------------------------------------------------------+---------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------+

.. note::

   To facilitate user permission management, use fine-grained policies rather than RBAC policies. In fine-grained policies, the Deny action takes precedence over other actions.

   -  A user has permission to synchronize IAM users only when the user has the Tenant Administrator role or has the Server Administrator, Tenant Guest, and MRS Administrator roles at the same time.
   -  A user with the **action:mrs:cluster:syncUser** policy has permission to synchronize IAM users.

Procedure
---------

#. Create a user and authorize the user to use MRS. For details, see :ref:`Creating an MRS User <mrs_01_0453>`.

#. Log in to the MRS management console and create a cluster. For details, see :ref:`Creating a Custom Cluster <mrs_01_0513>`.

#. In the left navigation pane, choose **Clusters** > **Active Clusters**. Click the cluster name to go to the cluster details page.

#. .. _mrs_01_0495__li6999515311:

   In the **Basic Information** area on the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.

#. After a synchronization request is sent, choose **Operation Logs** in the left navigation pane on the MRS console to check whether the synchronization is successful. For details about the logs, see :ref:`Viewing MRS Operation Logs <en-us_topic_0012808265>`.

#. After the synchronization is successful, use the user synchronized with IAM to perform subsequent operations.

   .. note::

      -  When the policy of the user group to which the IAM user belongs changes from **MRS ReadOnlyAccess** to **MRS CommonOperations**, **MRS FullAccess**, or **MRS Administrator**, wait for 5 minutes until the new policy takes effect after the synchronization is complete because the **SSSD** (System Security Services Daemon) cache of cluster nodes needs time to be updated. Then, submit a job. Otherwise, the job may fail to be submitted.
      -  When the policy of the user group to which the IAM user belongs changes from **MRS CommonOperations**, **MRS FullAccess**, or **MRS Administrator** to **MRS ReadOnlyAccess**, wait for 5 minutes until the new policy takes effect after the synchronization is complete because the **SSSD** cache of cluster nodes needs time to be updated.
      -  After you click **Synchronize** on the right side of **IAM User Sync**, the cluster details page is blank for a short time, because user data is being synchronized. The page will be properly displayed after the data synchronization is complete.

   -  Submitting jobs in a security cluster: Users can submit jobs using the job management function on the GUI in the security cluster. For details, see :ref:`Running a MapReduce Job <mrs_01_0052>`.
   -  All tabs are displayed on the cluster details page, including **Components**, **Tenants**, and **Backups & Restorations**.
   -  Logging in to Manager

      a. Log in to Manager as user **admin**. For details, see :ref:`Accessing Manager <mrs_01_0128>`.

      b. .. _mrs_01_0495__li169901714175:

         Initialize the password of the user synchronized with IAM. For details, see :ref:`Initializing the Password of a System User <mrs_01_0351>`.

      c. Modify the role bound to the user group to which the user belongs to control user permissions on Manager. For details, see :ref:`Related Tasks <mrs_01_0344__s855da92cb75446818be082dff6e197f1>`. For details about how to create and modify a role, see :ref:`Creating a Role <mrs_01_0343>`. After the component role bound to the user group to which the user belongs is modified, it takes some time for the role permissions to take effect.

      d. Log in to Manager using the user synchronized with IAM and the password after the initialization in :ref:`6.b <mrs_01_0495__li169901714175>`.

      .. note::

         If the IAM user's permission changes, go to :ref:`4 <mrs_01_0495__li6999515311>` to perform second synchronization. After the second synchronization, a system user's permissions are the union of the permissions defined in the IAM system policy and the permissions of roles added by the system user on Manager. After the second synchronization, a custom user's permissions are subject to the permissions configured on Manager.

         -  System user: If all user groups to which an IAM user belongs are bound to system policies (RABC policies and fine-grained policies belong to system policies), the IAM user is a system user.
         -  Custom user: If the user group to which an IAM user belongs is bound to any custom policy, the IAM user is a custom user.
