:original_name: mrs_01_0427.html

.. _mrs_01_0427:

Changing the Password of an Operation User
==========================================

Scenario
--------

Passwords of **Human-Machine** system users must be regularly changed to ensure MRS cluster security. This section describes how to change your passwords on MRS Manager.

If a new password policy needs to be used for the password modified by the user, follow instructions in :ref:`Modifying a Password Policy <mrs_01_0430>` to modify the password policy and then perform the following operations to modify the password.

Impact on the System
--------------------

If you have downloaded a user authentication file, download it again and obtain the keytab file after changing the password of the MRS cluster user.

Prerequisites
-------------

-  You have obtained the current password policies from the administrator.
-  You have obtained the MRS Manager access address from the administrator.

Procedure
---------

#. On MRS Manager, move the mouse cursor to |image1| in the upper right corner.

   On the menu that is displayed, select **Change Password**.

#. Fill in the **Old Password**, **New Password**, and **Confirm Password**. Click **OK**.

   For the cluster, the default password complexity requirements are as follows:

   -  The password must contain 8 to 32 characters.
   -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, spaces, and special characters (``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``).
   -  The password cannot be the username or the reverse username.

.. |image1| image:: /_static/images/en-us_image_0000001295898372.jpg
