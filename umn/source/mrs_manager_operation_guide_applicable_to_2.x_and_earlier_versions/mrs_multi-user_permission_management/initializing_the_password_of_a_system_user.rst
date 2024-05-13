:original_name: mrs_01_0351.html

.. _mrs_01_0351:

Initializing the Password of a System User
==========================================

Scenario
--------

This section describes how to initialize a password on Manager if a user forgets the password or the password of a public account needs to be changed regularly. After password initialization, the user must change the password upon the first login. This operation is supported only in clusters with Kerberos authentication enabled or common clusters with the EIP function enabled.

.. note::

   The operations described in this section apply only to clusters of versions earlier than MRS 3.x.

   For clusters of **MRS 3.\ x** or later, see :ref:`Initializing a Password <admin_guide_000144>`.

Impact on the System
--------------------

If you have downloaded a user authentication file, download it again and obtain the keytab file after initializing the password of the MRS cluster user.

Initializing the Password of a Human-Machine User
-------------------------------------------------

#. Access MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`.

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

#. Prepare a client based on service conditions and log in to the node with the client installed.

#. Run the following command to switch the user:

   **sudo su - omm**

#. Run the following command to switch to the client directory, for example, **/opt/Bigdata/client**:

   **cd /opt/Bigdata/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to log in to the console as user **kadmin/admin**:

   .. note::

      The default password of user **kadmin/admin** is **KAdmin@123**, which will expire upon your first login. Change the password as prompted and keep the new password secure.

   **kadmin -p kadmin/admin**

#. Run the following command to reset the password of a component running user. This operation takes effect on all servers:

   **cpw** *Component running user name*

   For example, **cpw oms/manager**.

   For the cluster, the default password complexity requirements are as follows:

   -  The password must contain 8 to 32 characters.
   -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, spaces, and special characters (``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``).
   -  The password cannot be the username or the reverse username.
