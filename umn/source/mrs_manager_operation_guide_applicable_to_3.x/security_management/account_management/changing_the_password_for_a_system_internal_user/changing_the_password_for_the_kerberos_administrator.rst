:original_name: admin_guide_000253.html

.. _admin_guide_000253:

Changing the Password for the Kerberos Administrator
====================================================

Scenario
--------

It is recommended that the administrator periodically change the password of Kerberos administrator **kadmin** to improve the system O&M security.

If the user password is changed, the OMS Kerberos administrator password is changed as well.

Prerequisites
-------------

You have installed the client on any node in the cluster and obtained the IP address of the node.

Procedure
---------

#. Log in to the node where the client is installed as user **root**.

#. Run the following command to go to the client directory, for example, **/opt/hadoopclient**:

   **cd /opt/hadoopclient**

#. Run the following command to set environment variables:

   **source bigdata_env**

#. Run the following command to change the password for **kadmin/admin**. The password changing takes effect on all servers.

   **kpasswd kadmin/admin**

   The password must meet the following complexity requirements by default:

   -  The password contains at least 8 characters.
   -  The password contains at least four types of the following characters: Uppercase letters, lowercase letters, digits, spaces, and special characters which can only be\ :literal:`~`!?,.;-_'(){}[]/<>@#$%^&*+|\\=.`
   -  The password cannot be the same as the username or the username spelled backwards.
   -  The password cannot be a common easily-cracked passwords, for example, **Admin@12345**.
   -  The password cannot be the same as the password used in the last *N* times. *N* indicates the value of **Repetition Rule** in :ref:`Configuring Password Policies <admin_guide_000150>`.
