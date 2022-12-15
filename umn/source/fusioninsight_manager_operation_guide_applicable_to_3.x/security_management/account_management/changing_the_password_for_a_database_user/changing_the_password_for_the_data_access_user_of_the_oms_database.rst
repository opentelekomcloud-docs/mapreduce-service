:original_name: admin_guide_000260.html

.. _admin_guide_000260:

Changing the Password for the Data Access User of the OMS Database
==================================================================

Scenario
--------

It is recommended that the administrator periodically change the password of the user accessing the OMS database to improve the system O&M security.

Impact on the System
--------------------

The OMS service needs to be restarted for the new password to take effect. The service is unavailable during the restart.

Procedure
---------

#. On FusionInsight Manager, choose **System** > **OMS** > **gaussDB** > **Change Password**.

#. Locate the row where user **omm** is located and click **Change Password** in the **Operation** column.

#. In the displayed window, enter the password of the current login user and click **OK**.

#. Enter the old and new passwords as prompted.

   The password complexity requirements are as follows:

   -  The password must contain 8 to 32 characters.
   -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, and special characters which can only be (``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``).
   -  The password cannot be the same as the username or the username spelled backwards.
   -  The password cannot be the same as the last 20 historical passwords.

#. Click **OK**. Wait until the system displays a message indicating that the operation is successful.

#. Locate the row where user **omm** is located and click **Restart OMS Service** in the **Operation** column.

#. In the displayed window, enter the password of the current login user and click **OK**.

#. In the displayed restart confirmation dialog box, click **OK** to restart the OMS service.
