:original_name: mrs_01_0428.html

.. _mrs_01_0428:

Initializing the Password of a System User
==========================================

Scenario
--------

This section describes how to initialize a password on MRS Manager if a user forgets the password or the password of a public account needs to be changed regularly. After password initialization, the user must change the password upon the first login.

Impact on the System
--------------------

If you have downloaded a user authentication file, download it again and obtain the keytab file after initializing the password of the MRS cluster user.

Initializing the Password of a Human-Machine User
-------------------------------------------------

#. On MRS Manager, click **System**.

#. In the **Permission** area, click **Manage User**.

#. Locate the row that contains the user whose password is to be initialized, choose **More** > **Initialize password**, and change the password as prompted.

   In the window that is displayed, enter the password of the current administrator account and click **OK**. Then in **Initialize password**, click **OK**.

   For the cluster, the default password complexity requirements are as follows:

   -  The password must contain 8 to 32 characters.
   -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, spaces, and special characters (``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``).
   -  The password cannot be the username or the reverse username.

Initializing the Password of a Machine-Machine User
---------------------------------------------------

#. Prepare a client based on service conditions and log in to the node where the client is installed.

#. Run the following command to switch the user:

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

   For example, **cpw oms/manager**.

   For the cluster, the default password complexity requirements are as follows:

   -  The password must contain 8 to 32 characters.
   -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, spaces, and special characters (``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``).
   -  The password cannot be the username or the reverse username.
