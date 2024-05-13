:original_name: admin_guide_000254.html

.. _admin_guide_000254:

Changing the Password for the OMS Kerberos Administrator
========================================================

Scenario
--------

It is recommended that the administrator periodically change the password of OMS Kerberos administrator **kadmin** to improve the system O&M security.

If the user password is changed, the Kerberos administrator password is changed as well.

Procedure
---------

#. Log in to any management node in the cluster as user **omm**.

#. Run the following command to go to the related directory:

   **cd ${BIGDATA_HOME}/om-server/om/meta-0.0.1-SNAPSHOT/kerberos/scripts**

#. Run the following command to set environment variables:

   **source component_env**

#. Run the following command to change the password for **kadmin/admin**. The password changing takes effect on all servers.

   **kpasswd kadmin/admin**

   The password must meet the following complexity requirements by default:

   -  The password contains at least 8 characters.
   -  The password contains at least four types of the following characters: uppercase letters, lowercase letters, digits, and special characters can only be :literal:`~`!?,.:;-_'(){}[]/<>@#$%^&*+|\\=.`
   -  The password cannot be the same as the username or the username spelled backwards.
   -  The password cannot be a common easily-cracked passwords, for example, **Admin@12345**.
   -  The password cannot be the same as the password used in the last *N* times. *N* indicates the value of **Repetition Rule** in :ref:`Configuring Password Policies <admin_guide_000150>`.
