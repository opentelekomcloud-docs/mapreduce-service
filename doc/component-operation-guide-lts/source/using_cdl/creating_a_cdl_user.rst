:original_name: mrs_01_24234.html

.. _mrs_01_24234:

Creating a CDL User
===================

Scenario
--------

Before using the CDL service, a cluster administrator needs to create a user and grant operation permissions to the user to meet service requirements.

CDL users are classified into administrators and common users. The default CDL user group for administrators and common users is **cdladmin** and **cdl**, respectively.

-  Users associated with the **cdladmin** user group can perform any CDL operations.
-  Users associated with the **cdl** user group can perform creation and query operations on CDL.

If Ranger authentication is enabled and you need to configure the creation, execution, query, or deletion permission for CDL users, see :ref:`Adding a Ranger Access Permission Policy for CDL <mrs_01_24245>`.

If Ranger authentication is manually disabled for a cluster, enable Ranger authentication by referring to :ref:`Enabling Ranger Authentication <mrs_01_2393>`.

.. note::

   This section applies only to clusters with Kerberos authentication enabled.

Procedure
---------

#. Log in to FusionInsight Manager.
#. Choose **System**. On the navigation pane on the left, choose **Permission** > **User** and click **Create**.
#. Enter a username, for example, **cdl_admin**.
#. Set **User Type** to **Human-Machine**.
#. Set **Password** and confirm your password.
#. Set **User Group** and **Primary Group**.

   -  CDL administrator permissions: Add the **cdladmin** user group and set it to the primary group.
   -  Common CDL user permissions: Add the **cdl** user group and set it to the primary group.

#. Click **OK**.
