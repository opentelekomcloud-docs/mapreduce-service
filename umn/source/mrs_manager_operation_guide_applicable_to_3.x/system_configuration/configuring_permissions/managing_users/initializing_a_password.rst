:original_name: admin_guide_000144.html

.. _admin_guide_000144:

Initializing a Password
=======================

Scenario
--------

If a user forgets the password or the public account password needs to be changed periodically, you can initialize the password on MRS Manager. After the password is initialized, the system user needs to change the password upon first login.

.. note::

   This operation applies only to human-machine users.

Procedure
---------

#. Log in to MRS Manager.

#. Choose **System** > **Permission** > **User**.

#. Locate the row that contains the target user, click **More**, and select **Initialize Password**. In the displayed dialog box, enter the password of the current login user and click **OK**. In the **Initialize Password** dialog box, click **OK**.

#. Set **New Password** and **Confirm Password**, and click **OK**.

   The password must meet the following complexity requirements by default:

   -  The password contains at least 8 characters.
   -  The password must contain at least four types of the following characters: uppercase letters, lowercase letters, digits, spaces, and special characters :literal:`\`~!@#$%^&*()-_=+|[{}];',<.>/\\?`.
   -  The password cannot be the same as the username or the username spelled backwards.
   -  The password cannot be a common easily-cracked password.
   -  The password cannot be the same as the password used in the latest *N* times. *N* indicates the value of **Repetition Rule** configured in :ref:`Configuring Password Policies <admin_guide_000150>`.
