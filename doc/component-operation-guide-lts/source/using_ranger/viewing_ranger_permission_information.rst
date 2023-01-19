:original_name: mrs_01_1854.html

.. _mrs_01_1854:

Viewing Ranger Permission Information
=====================================

You can view Ranger permission settings, such as users, user groups, and roles.


Viewing Ranger Permission Information
-------------------------------------

#. Log in to the Ranger management page as the Ranger administrator.
#. Choose **Settings** > **Users**/**Groups**/**Roles** to view information about users, user groups, or roles in the system.

   -  Users: displays all user information synchronized from LDAP or OS to Ranger.
   -  Groups: displays information about all user groups and role information synchronized from LDAP or OS to Ranger.
   -  Roles: displays information about roles created in Ranger.

   .. note::

      -  The users, roles, user groups created on FusionInsight Manager are automatically synchronized to Ranger periodically. The default period is 300,000 milliseconds (5 minutes). After roles and user groups in FusionInsight Manager are synchronized to Ranger, they become user groups. Only roles and user groups that are associated with users can be automatically synchronized to Ranger.
      -  The role created on the Ranger page is a set of users or user groups, which is used to flexibly set the permission access policies of components. The role is different from that on FusionInsight Manager.

Adjusting Ranger User Types
---------------------------

#. Log in to the Ranger management page.

   To change the Ranger user type, you must log in as an **admin** user. For details about the user types, see :ref:`Ranger User Type <mrs_01_1850__en-us_topic_0000001219350647_section2695135412818>`.

#. Choose **Settings** > **Users**/**Groups**/**Roles**. In the list of users, click the name of the user whose type you want to change.

#. Set **Select Role** to the type to be modified.

#. Click **Save**.

Creating a Ranger Role
----------------------

The Ranger administrator can flexibly configure permission access policies for components based on users, user groups, or roles. User and user group information is automatically synchronized from LDAP, and roles can be manually added.

#. Log in to the Ranger management page.

#. Choose **Settings** > **Users**/**Groups**/**Roles** > **Roles** > **Add New Role**.

#. Enter the role name and description as prompted.

#. Add users, user groups, and sub-roles to the role.

   -  In the **Users** area, select a created user in the system and click **Add Users**.
   -  In the **Groups** area, select a created user group and click **Add Group**.
   -  In the **Roles** area, select a created role in the system and click **Add Role**.

   |image1|

#. Click **Save**. The role is added successfully.

.. |image1| image:: /_static/images/en-us_image_0000001296060048.png
