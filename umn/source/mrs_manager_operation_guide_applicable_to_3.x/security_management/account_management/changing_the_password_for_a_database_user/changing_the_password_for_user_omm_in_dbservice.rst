:original_name: admin_guide_000354.html

.. _admin_guide_000354:

Changing the Password for User omm in DBService
===============================================

#. Log in to the active DBService node as user **root**.

   .. note::

      The password of user **omm** for the DBService database cannot be changed on the standby DBService node. Change the password on the active DBService node only.

#. Run the following command to switch to another user:

   **su - omm**

#. Run the following command to go to the related directory:

   **source $DBSERVER_HOME/.dbservice_profile**

   **cd** **${DBSERVICE_SOFTWARE_DIR}/\ sbin/**

#. Run the following command to change the password of user **omm**:

   **sh modifyDBPwd.sh**

#. Enter the old password of user **omm** and enter a new password twice.

   The password complexity requirements are as follows:

   -  The password contains 8 to 32 characters.
   -  The password contains at least three types of the following: uppercase letters, lowercase letters, digits, and special characters which can only be (``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``).
   -  The password cannot be the same as the username or the username spelled backwards.
   -  The password cannot be the same as the last 20 historical passwords.

   If the following information is displayed, the password is changed successfully.

   .. code-block::

      Successful to modify password.
