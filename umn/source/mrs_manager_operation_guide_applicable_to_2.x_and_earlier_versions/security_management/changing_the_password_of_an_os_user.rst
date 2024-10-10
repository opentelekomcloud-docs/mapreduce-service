:original_name: mrs_01_0562.html

.. _mrs_01_0562:

Changing the Password of an OS User
===================================

Scenario
--------

This section describes how to periodically change the login passwords of the OS users **omm**, **ommdba**, and **root** on MRS cluster nodes to improve the system O&M security.

Passwords of users **omm**, **ommdba**, and **root** on each node can be different.

Procedure
---------

#. Log in to the **Master1** node and then log in to other nodes whose OS user passwords need to be changed.

#. Run the following command to switch to user **root**:

   **sudo su - root**

3. Run the following command to change the passwords of users **omm**, **ommdba**, or **root**:

   **passwd omm**

   **passwd ommdba**

   **passwd root**

   For example, if you run the **omm:passwd** command, the system displays the following information:

   .. code-block::

      Changing password for user omm.
      New password:

   Enter a new password. The password change policies for an OS vary according to the OS that is used.

   .. code-block::

      Retype new password:
      passwd: all authentication tokens updated successfully.

   .. note::

      The default password complexity requirements of the MRS cluster are as follows:

      -  The password must contain at least eight characters.
      -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, spaces, and special characters ``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``.
      -  The new password cannot be the same as last five historical passwords.
