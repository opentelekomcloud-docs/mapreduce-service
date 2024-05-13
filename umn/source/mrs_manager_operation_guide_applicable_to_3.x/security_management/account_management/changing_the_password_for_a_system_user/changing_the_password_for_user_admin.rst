:original_name: admin_guide_000250.html

.. _admin_guide_000250:

Changing the Password for User admin
====================================

Scenario
--------

User **admin** is the system administrator account of MRS Manager. You are advised to periodically change the password on MRS Manager to improve system security.

Procedure
---------

#. Log in to MRS Manager.

   User **admin** is required for login.

#. Move the cursor to **Hello, admin** in the upper right corner of the page.

   In the displayed menu, click **Change Password**.

#. Set **Old Password**, **New Password**, and **Confirm Password**, and click **OK**.

   The password must meet the following complexity requirements by default:

   -  The password contains 8 to 64 characters.
   -  The password contains at least four types of the following characters: Uppercase letters, lowercase letters, digits, spaces, and special characters which can only be :literal:`~`!?,.;-_'(){}[]/<>@#$%^&*+|\\=.`
   -  The password cannot be the same as the username or the username spelled backwards.
   -  The password cannot be a common easily-cracked passwords.
   -  The password cannot be the same as the password used in the last *N* times. *N* indicates the value of **Repetition Rule** in :ref:`Configuring Password Policies <admin_guide_000150>`.
