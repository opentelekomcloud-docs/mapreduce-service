:original_name: mrs_03_1249.html

.. _mrs_03_1249:

How Do I Query and Change the Password Validity Period of an Account?
=====================================================================

Querying the Password Validity Period
-------------------------------------

**Querying the password validity period of a component running user (human-machine user or machine-machine user):**

#. Log in to the node where the client is installed as the client installation user.

#. Run the following command to switch to the client directory, for example, **/opt/Bigdata/client**:

   **cd /opt/Bigdata/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. Run the following command and enter the password of user **kadmin/admin** to log in to the kadmin console:

   **kadmin -p kadmin/admin**

   .. note::

      The default password of user **kadmin/admin** is **Admin@123**. Change the password upon your first login or as prompted and keep the new password secure.

#. Run the following command to view the user information:

   **getprinc** *Internal system username*

   Example: **getprinc user1**

   .. code-block::

      kadmin:  getprinc user1
      ......
      Expiration date: [never]
      Last password change: Sun Oct 09 15:29:54 CST 2022
      Password expiration date: [never]
      ......

**Querying the password validity period of an OS user:**

#. Log in to any master node in the cluster as user **root**.

#. Run the following command to view the password validity period (value of **Password expires**):

   **chage -l** *Username*

   For example, to view the password validity period of user **root**, run the **chage -l** **root** command. The command output is as follows:

   .. code-block:: console

      [root@xxx ~]#chage -l root
      Last password change                                    : Sep 12, 2021
      Password expires                                        : never
      Password inactive                                       : never
      Account expires                                         : never
      Minimum number of days between password change          : 0
      Maximum number of days between password change          : 99999
      Number of days of warning before password expires       : 7

Changing the Password Validity Period
-------------------------------------

-  The password of a machine-machine user is randomly generated and never expires by default.
-  The password validity period of a human-machine user can be changed by modifying the password policy on Manager.
