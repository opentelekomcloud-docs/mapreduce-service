:original_name: admin_guide_000420.html

.. _admin_guide_000420:

Changing the OS User Password Validity Period
=============================================

Scenario
--------

By default, the password validity period of an OS user is 90 days. This topic describes how to change the validity period.

You are advised to periodically change a user's login password of the cluster node operating system to improve system O&M security.

Procedure
---------

#. Log in to the node where you want to change the password validity period of the OS user password as the **root** user.
#. Change the OS user password validity period.

   -  **Legacy users**

      Run the following command to change the password validity period:

      **chage -M**\ *Validity period (days) user_name*

      .. note::

         -  *Validity period (days)*: how many days the password is valid since its creation. If this parameter is set to **99999**, the password never expires. Set this parameter based on the site requirements.
         -  *user_name*: OS user whose validity period you want to change, for example, **ommdba**.
         -  You are advised to set this parameter based on service demands and periodically change the user password.

   -  **New users**

      Run the following command to edit the file and change the value of **PASS_MAX_DAYS**, which indicates the password validity period, in days. If the value is changed to **99999**, the password never expires.

      **vi /etc/login.defs**
