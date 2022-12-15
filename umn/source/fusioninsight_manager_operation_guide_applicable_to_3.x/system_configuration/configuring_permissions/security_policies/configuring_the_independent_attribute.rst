:original_name: admin_guide_000151.html

.. _admin_guide_000151:

Configuring the Independent Attribute
=====================================

Scenario
--------

User **admin** or administrators who are bound to the Manager_administrator role can configure the independent attribute on FusionInsight Manager so that common users (all service users in the cluster) can set or cancel their own independent attributes.

After the independent attribute option is toggled on, service users need to log in to the system and set the independent attribute.

Constraints
-----------

-  Administrators cannot set or cancel the independent attribute of a user.
-  Administrators cannot obtain the authentication credentials of independent users.

Prerequisites
-------------

You have obtained the required administrator username and password.

Procedure
---------

**Toggling On or Off the Independent Attribute**

#. Log in to FusionInsight Manager as user **admin** or a user bound to the Manager_administrator role.
#. Choose **System** > **Permission** > **Security Policy** > **Independent Configurations**.
#. Toggle on or off **Independent Attribute**, enter the password as prompted, and click **OK**.
#. After the identity is authenticated, wait until the OMS configuration is modified and click **Finish**.

   .. note::

      After the independent attribute is disabled:

      -  A user who has the attribute can cancel it from the drop-down list of the username in the upper right corner of the page. The user cannot set the independent attribute again once it is cancelled. After the attribute is cancelled, existing independent tables will retain the attribute. However, the user cannot create independent tables again.
      -  Users without this attribute cannot set or cancel the attribute.

**Configuring the Independent Attribute**

5. Log in to FusionInsight Manager as a service user.

   .. important::

      Administrators cannot initialize the password of the user after the independent attribute is set. If the user password is forgotten, the password cannot be retrieved.

      User **admin** cannot set the independent attribute.

6. Move the cursor to the username in the upper right corner of the page.
7. Select **Set Independent** or **Cancel Independent**.

   .. note::

      -  If the independent attribute is toggled on and has been set for the service user, **Cancel Independent** is displayed.
      -  If the independent attribute is toggled on but has been cancelled for the service user, **Set Independent** is displayed.
      -  If the independent attribute is toggled off but has been set for the service user, **Cancel Independent** is displayed.
      -  If the independent attribute is toggled off and has been cancelled for the service user, no option related to the independent attribute is displayed.

8. Enter the password as prompted and click **OK**.
9. After the identity is authenticated, click **OK** in the dialog box.
