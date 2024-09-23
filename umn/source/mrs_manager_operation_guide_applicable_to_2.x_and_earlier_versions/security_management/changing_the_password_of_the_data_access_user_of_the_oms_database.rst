:original_name: mrs_01_0568.html

.. _mrs_01_0568:

Changing the Password of the Data Access User of the OMS Database
=================================================================

Scenario
--------

This section describes how to periodically change the password of the data access user of the OMS database to improve the system O&M security.

Impact on the System
--------------------

The OMS service needs to be restarted for the new password to take effect. The service is unavailable during the restart.

Procedure
---------

#. On MRS Manager, click **System**.

#. In the **Permission** area, click **Change OMS Database Password**.

#. Locate the row that contains user **omm**, and click **Change password** in the **Operation** column.

   The password complexity requirements are as follows:

   -  The password must contain 8 to 32 characters.
   -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, and special characters ``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``.
   -  The password cannot be the username or the reverse username.
   -  The password cannot be the same as the last 20 historical passwords.

#. Click **OK**. When **Operation successful** is displayed, click **Finish**.

#. Locate the row that contains user **omm**, and click **Restart the OMS service** in the **Operation** column to restart the OMS database.

   .. note::

      If the password is changed but the OMS database is not restarted, the status of user **omm** changes to **Waiting to restart** and the password cannot be changed until the OMS database is restarted.

#. In the displayed dialog box, select **I have read the information and understand the impact**. Click **OK**, and restart the OMS service.
