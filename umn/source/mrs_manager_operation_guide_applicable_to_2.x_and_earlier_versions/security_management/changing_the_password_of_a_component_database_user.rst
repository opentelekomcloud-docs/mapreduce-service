:original_name: mrs_01_0569.html

.. _mrs_01_0569:

Changing the Password of a Component Database User
==================================================

Scenario
--------

This section describes how to periodically change the password of the component database user to improve the system O&M security.

Impact on the System
--------------------

The services need to be restarted for the new password to take effect. The services are unavailable during the restart.

Procedure
---------

#. On MRS Manager, click **Services** and click the name of the database user service to be modified.

#. Determine the component database user whose password is to be changed.

   -  To change the password of the DBService database user, go to :ref:`3 <mrs_01_0569__en-us_topic_0042008033_li30220842102536>`.
   -  To change the password of the Loader, Hive, or Hue database user, stop the service first and then execute :ref:`3 <mrs_01_0569__en-us_topic_0042008033_li30220842102536>`.

   Click **Stop Service**.

#. .. _mrs_01_0569__en-us_topic_0042008033_li30220842102536:

   Choose **More** > **Change Password**.

#. Enter the old and new passwords as prompted.

   The password complexity requirements are as follows:

   -  The password of the DBService database user contains 16 to 32 characters. The password of the Loader, Hive, or Hue database user contains 8 to 32 characters.
   -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, and special characters (``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``).
   -  The password cannot be the username or the reverse username.
   -  The password cannot be the same as the last 20 historical passwords.

#. Click **OK**. The system automatically restarts the corresponding service. When **Operation successful** is displayed, click **Finish**.
