:original_name: mrs_01_0563.html

.. _mrs_01_0563:

Changing the password of user **admin**
=======================================

This section describes how to periodically change the password of cluster user **admin** to improve the system O&M security.

If the password is changed, the downloaded user credential will be unavailable. Download the authentication credential again, and replace the old one.

Changing the Password of User admin on the Cluster Node
-------------------------------------------------------

#. Update the client of the active management node. For details, see :ref:`Updating a Client (Versions Earlier Than 3.x) <mrs_01_0089>`.

#. Log in to the active management node.

#. (Optional) To change the password as user **omm**, run the following command to switch the user:

   **sudo su - omm**

#. Run the following command to switch to the client directory, for example, **/opt/client**.

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to change the password of user **admin**: This operation takes effect in the whole cluster.

   **kpasswd admin**

   Enter the old password and then enter a new password twice.

   For the MRS 1.6.3 or later cluster, the default password complexity requirements are as follows:

   -  The password must contain at least eight characters.
   -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, spaces, and special characters (``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``).
   -  The password cannot be the username or the reverse username.

Changing the Password of User admin on MRS Manager
--------------------------------------------------

You can change the password of user **admin** on MRS Manager only for clusters with Kerberos authentication enabled and clusters with Kerberos authentication disabled but the EIP function enabled.

#. Log in to MRS Manager as user **admin**.
#. Click the username in the upper right corner of the page and choose **Change Password**.
#. On the **Change Password** page, set **Old Password**, **New Password**, and **Confirm Password**.

   .. note::

      The default password complexity requirements are as follows:

      -  The password must contain 8 to 32 characters.
      -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, spaces, and special characters (``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``).
      -  The password cannot be the username or the reverse username.

#. Click **OK**. Log in to MRS Manager with the new password.

Resetting the Password for User **admin**
-----------------------------------------

#. Log in to the **Master1** node.

#. (Optional) To change the password as user **omm**, run the following command to switch the user:

   **sudo su - omm**

#. Run the following command to switch to the client directory, for example, **/opt/client**:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to log in to the console as user **kadmin/admin**:

   **kadmin -p kadmin/admin**

   .. note::

      The default password of user **kadmin/admin** is **KAdmin@123**, which will expire upon your first login. Change the password as prompted and keep the new password secure.

#. Run the following command to reset the password of a component running user. This operation takes effect for all servers.

   **cpw** *Component running user name*

   For example, to reset the password of user admin, run the **cpw admin** command.

   For the cluster, the default password complexity requirements are as follows:

   -  The password must contain 8 to 32 characters.
   -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, spaces, and special characters (``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``).
   -  The password cannot be the username or the reverse username.
