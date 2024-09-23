:original_name: mrs_01_0564.html

.. _mrs_01_0564:

Changing the Password of the Kerberos Administrator
===================================================

Scenario
--------

This section describes how to periodically change the password of the Kerberos administrator **kadmin** of the MRS cluster to improve the system O&M security.

If the password is changed, the downloaded user credential will be unavailable. Download the authentication credential again, and replace the old one.

Prerequisites
-------------

A client has been prepared on the **Master1** node.

Procedure
---------

#. Log in to the **Master1** node.

#. (Optional) To change the password as user **omm**, run the following command to switch the user:

   **sudo su - omm**

#. Run the following command to switch to the client directory, for example, **/opt/client**.

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command to change the password of **kadmin/admin**. This operation takes effect for all servers.

   **kpasswd kadmin/admin**

   For the cluster, the default password complexity requirements are as follows:

   -  The password must contain at least eight characters.
   -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, spaces, and special characters ``'~!@#$%^&*()-_=+\|[{}];:'",<.>/?``.
   -  The password cannot be the username or the reverse username.
