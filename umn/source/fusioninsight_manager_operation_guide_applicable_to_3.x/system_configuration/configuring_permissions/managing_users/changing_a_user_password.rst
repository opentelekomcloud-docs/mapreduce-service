:original_name: admin_guide_000143.html

.. _admin_guide_000143:

Changing a User Password
========================

Scenario
--------

For security purposes, the password of a human-machine user must be changed periodically.

If users have the permission to use FusionInsight Manager, they can change their passwords on FusionInsight Manager.

If users do not have the permission to use FusionInsight Manager, they can change their passwords on the client.

Prerequisites
-------------

-  You have obtained the current password policy.
-  The user has installed the client on any node in the cluster and obtained the IP address of the node. The password of the client installation user can be obtained from the administrator.

Changing the Password on FusionInsight Manager
----------------------------------------------

#. Log in to FusionInsight Manager.

#. Move the cursor to the username in the upper right corner of the page.

   On the user account drop-down menu, choose **Change Password**.

#. On the displayed page, set **Current Password**, **New Password**, and **Confirm Password**, and click **OK**.

   By default, the password must meet the following complexity requirements:

   -  The password contains at least 8 characters.
   -  The password must contain at least four types of the following characters: uppercase letters, lowercase letters, digits, spaces, and special characters (:literal:`\`~!@#$%^&*()-_=+|[{}];',<.>/\\?`).
   -  The password cannot be the same as the username or the username spelled backwards.
   -  The password cannot be a common easily-cracked password.
   -  The password cannot be the same as the password used in the latest *N* times. *N* indicates the value of **Repetition Rule** configured in :ref:`Configuring Password Policies <admin_guide_000150>`.

Changing the Password on the Client
-----------------------------------

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to switch to the client directory, for example, **/opt/client**:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Change the user password. This operation takes effect for all servers.

   **kpasswd** *System username*

   For example, if you want to change the password of system user **test1**, run the **kpasswd test1** command.

   By default, the password must meet the following complexity requirements:

   -  The password contains at least 8 characters.
   -  The password must contain at least four types of the following characters: uppercase letters, lowercase letters, digits, spaces, and special characters (:literal:`\`~!@#$%^&*()-_=+|[{}];',<.>/\\?`).
   -  The password cannot be the same as the username or the username spelled backwards.
   -  The password cannot be a common easily-cracked password.
   -  The password cannot be the same as the password used in the latest *N* times. *N* indicates the value of **Repetition Rule** configured in :ref:`Configuring Password Policies <admin_guide_000150>`.

   .. note::

      If an error occurs during the running of the **kpasswd** command, try the following operations:

      -  Stop the SSH session and start it again.
      -  Run the **kdestroy** command and then run the **kpasswd** command again.
