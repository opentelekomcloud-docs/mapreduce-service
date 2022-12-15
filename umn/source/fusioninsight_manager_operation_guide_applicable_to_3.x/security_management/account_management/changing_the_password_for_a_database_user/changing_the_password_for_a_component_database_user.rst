:original_name: admin_guide_000261.html

.. _admin_guide_000261:

Changing the Password for a Component Database User
===================================================

Scenario
--------

It is recommended that the administrator periodically change the password for each component database user to improve the system O&M security.

.. note::

   This section applies only to MRS 3.1.0. For versions later than MRS 3.1.0, see :ref:`Resetting the Component Database User Password <admin_guide_000363>`.

Impact on the System
--------------------

The services need to be restarted for the new password to take effect. The services are unavailable during the restart.

Procedure
---------

#. On FusionInsight Manager, click **Cluster**, click the name of the desired cluster, and click **Services**.

#. Determine the component database user whose password is to be changed.

   For details about how to change the password of database user **omm** of DBService, perform operations in :ref:`Changing the Password for User omm in DBService <admin_guide_000354>`. To change the passwords of database users of other components, you need to stop services first and then perform the operations in :ref:`3 <admin_guide_000261__li12756790114651>`.

#. .. _admin_guide_000261__li12756790114651:

   Click the service whose database user password is to be changed, and choose **More** > **Change Database Password**. On the displayed page, enter the password of the current login user and click **OK**.

#. Enter the old and new passwords as prompted.

   The password complexity requirements are as follows:

   -  The database user password contains 8 to 32 characters.
   -  The password contains at least three types of the following: uppercase letters, lowercase letters, digits, and special characters which can only be (``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``).
   -  The password cannot be the same as the username or the username spelled backwards.
   -  The password cannot be the same as the last 20 historical passwords.

#. Select "I have read the information and understand the impact" and click **OK**.

#. After the password is changed, choose **More** > **Restart Service**. In the displayed dialog box, enter the password of the current login user, click **OK**, and select **Restart the upper-layer services**. Click **OK** to restart the services.
