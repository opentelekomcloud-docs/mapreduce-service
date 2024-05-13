:original_name: admin_guide_000251.html

.. _admin_guide_000251:

Changing the Password for an OS User
====================================

Scenario
--------

During MRS Manager installation, the system automatically creates user **omm** and **ommdba** on each node in the cluster. Periodically change the login passwords of the OS users **omm** and **ommdba** of the cluster node to improve the system O&M security.

The passwords of users **omm** and **ommdba** of the nodes can be different.

Prerequisites
-------------

-  You have obtained the IP address of the node where the passwords of users **omm** and **ommdba** are to be changed.
-  You have obtained the password of user **root** before changing the passwords of users **omm** and **ommdba**.

Changing the Password of an OS User
-----------------------------------

#. Log in to the node where the password is to be changed as user **root**.

#. Run the following command to change the user password:

   **passwd** *ommdba*

   Red Hat system displays the following information:

   .. code-block::

      Changing password for user ommdba.
      New password:

#. Enter a new password. The policy for changing the password of an OS user varies according to the OS that is actually used.

   .. code-block::

      Retype New Password:
      Password changed.
