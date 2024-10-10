:original_name: admin_guide_000259.html

.. _admin_guide_000259:

Changing the Password of the OMS Database Administrator
=======================================================

Scenario
--------

It is recommended that the administrator periodically change the password of the OMS database administrator to improve the system O&M security.

Procedure
---------

#. Log in to the active management node as user **root**.

   .. note::

      The password of user **ommdba** cannot be changed on the standby management node. Otherwise, the cluster may not work properly. Change the password on the active management node only.

#. Run the following command to switch to another user:

   **su - omm**

#. Run the following command to go to the related directory:

   **cd $OMS_RUN_PATH/tools**

#. Run the following command to change the password for user **ommdba**:

   **mod_db_passwd ommdba**

#. Enter the old password of user **ommdba** and enter a new password twice.

   The password complexity requirements are as follows:

   -  The password contains 16 to 32 characters.
   -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, and special characters which can only be ``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``.
   -  The password cannot be the same as the username or the username spelled backwards.
   -  The password cannot be the same as the last 20 historical passwords.

   If the following information is displayed, the password is changed successfully.

   .. code-block::

      Congratulations, update [ommdba] password successfully.
