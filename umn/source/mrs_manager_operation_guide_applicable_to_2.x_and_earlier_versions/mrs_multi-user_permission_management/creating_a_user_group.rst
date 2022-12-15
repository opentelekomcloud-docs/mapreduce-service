:original_name: mrs_01_0344.html

.. _mrs_01_0344:

Creating a User Group
=====================

Scenario
--------

This section describes how to create user groups and specify their operation permissions on Manager. Management of single or multiple users can be unified in the user groups. After being added to a user group, users can obtain operation permissions owned by the user group.

Manager supports a maximum of 100 user groups.

.. note::

   The operations described in this section apply only to clusters of versions earlier than MRS 3.x.

   For clusters of **MRS 3.\ x** or later, see :ref:`Managing User Groups <admin_guide_000147>`.

Prerequisites
-------------

-  Administrators have learned service requirements and created roles required by service scenarios.
-  You have obtained a cluster with Kerberos authentication enabled or a common cluster with the EIP function enabled.

Procedure
---------

#. Access MRS Manager. For details, see :ref:`Accessing MRS Manager MRS 2.1.0 or Earlier) <mrs_01_0102>`.

#. On MRS Manager, click **System**.

#. In the **Permission** area, click **Manage User Group**.

#. Above the user group list, click **Create User Group**.

#. Input **Group Name** and **Description**.

   **Group Name** is mandatory and contains 3 to 20 characters. Only digits, letters, and underscores (_) are allowed. **Description** is optional.

#. In **Role**, click **Select and Add Role** to select and add specified roles.

   If you do not add the roles, the user group you are creating now does not have the permission to use MRS clusters.

#. Click **OK**.

.. _mrs_01_0344__s855da92cb75446818be082dff6e197f1:

Related Tasks
-------------

**Modifying a user group**

#. On MRS Manager, click **System**.
#. In the **Permission** area, click **Manage User Group**.
#. In the row of a user group to be modified, click **Modify**.

   .. note::

      If you change role permissions assigned to the user group, it takes 3 minutes to make new configurations take effect.

#. Click **OK**. The modification is complete.

**Deleting a user group**

#. On MRS Manager, click **System**.
#. In the **Permission** area, click **Manage User Group**.
#. In the row of the user group to be deleted, click **Delete**.
#. Click **OK**. The user group is deleted.
