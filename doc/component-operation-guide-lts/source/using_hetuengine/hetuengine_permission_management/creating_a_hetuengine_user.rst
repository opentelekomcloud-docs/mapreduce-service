:original_name: mrs_01_1714.html

.. _mrs_01_1714:

Creating a HetuEngine User
==========================

Scenarios
---------

Before using the HetuEngine service in a security cluster, a cluster administrator needs to create a user and grant operation permissions to the user to meet service requirements.

HetuEngine users are classified into administrators and common users. The default HetuEngine administrator group is **hetuadmin**, and the user group of HetuEngine common users is **hetuuser**.

-  Users associated with the **hetuadmin** user group can obtain the O&M administrator permissions on the HetuEngine HSConsole web UI and HetuEngine compute instance web UI.
-  Users associated with the **hetuuser** user group can obtain the SQL execution permission.

If Ranger authentication is enabled and you need to configure the permissions to manage databases, tables, and columns of data sources for a user after it is created, see :ref:`Adding a Ranger Access Permission Policy for HetuEngine <mrs_01_1862>`.

Prerequisites
-------------

Before using the HetuEngine service, ensure that the tenant to be associated with the HetuEngine user has been planned and created. For details about how to create and use a tenant in an MRS cluster.

.. note::

   Common users can only perform operations on and view information about clusters of the tenants associated with them.

Procedure
---------

**Creating a HetuEngine administrator**

#. Log in to FusionInsight Manager.
#. Choose **System** > **Permission** > **User** > **Create**.
#. Enter a username, for example, **hetu_admin**.
#. Set **User Type** to **Human-machine**.
#. Set **New Password** and **Confirm Password**.
#. In the **User Group** area, click **Add** to add the **hive**, **hetuadmin**, **hadoop**, **hetuuser**, and **yarnviewgroup** user groups for the user.
#. In the **Primary Group** drop-down list, select **hive** as the primary group.
#. In the **Role** area, click **Add** to assign the **default**, **System_administrator**, and desired tenant role permissions to the user.
#. Click **OK**.

**Creating a common HetuEngine user**

#. Log in to FusionInsight Manager.
#. Choose **System** > **Permission** > **User** > **Create**.
#. Enter a username, for example, **hetu_test**.
#. Set **User Type** to **Human-machine**.
#. Set **New Password** and **Confirm Password**.
#. In the **User Group** area, click **Add** to add the **hetuuser** user group for the user.

   .. note::

      -  Ranger authentication is enabled for the HetuEngine service in the MRS cluster by default. HetuEngine common users only need to be associated with the **hetuuser** user group. If Ranger authentication is disabled, you must associate the user with the **hive** user group and set it as the primary group. Otherwise, the HetuEngine service may be unavailable.
      -  If Ranger authentication is enabled and you need to configure the permissions to manage databases, tables, and columns of data sources for a user after it is created, see :ref:`Adding a Ranger Access Permission Policy for HetuEngine <mrs_01_1862>`.

#. In the **Role** area, click **Add** to assign the **default** or desired tenant role permissions to the user.
#. Click **OK**.
