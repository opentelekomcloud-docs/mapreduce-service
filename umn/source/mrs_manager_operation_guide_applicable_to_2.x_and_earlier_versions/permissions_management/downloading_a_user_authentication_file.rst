:original_name: mrs_01_0429.html

.. _mrs_01_0429:

Downloading a User Authentication File
======================================

Scenario
--------

When a user develops big data applications and runs them in an MRS cluster that supports Kerberos authentication, the user needs to prepare a user authentication file for accessing the MRS cluster. The keytab file in the authentication file can be used for user authentication.

This section describes how to download a user authentication file and export the keytab file on MRS Manager.

.. note::

   -  Before downloading a **Human-machine** user authentication file, change the password for the user on MRS Manager to make the initial password set by the administrator invalid. Otherwise, the exported keytab file cannot be used. For details, see :ref:`Changing the Password of an Operation User <mrs_01_0427>`.
   -  After a user password is changed, the exported keytab file becomes invalid, and you need to export a keytab file again.

Procedure
---------

#. On MRS Manager, click **System**.
#. In the **Permission** area, click **Manage User**.
#. In the row of the user for whom you want to export the keytab file, choose **More** > **Download authentication credential** to download the authentication file. After the file is automatically generated, save it to a specified path and keep it properly.
#. Open the authentication file with a decompression program.

   -  **user.keytab** indicates a user keytab file used for user authentication.
   -  **krb5.conf** indicates the configuration file of the authentication server. The application connects to the authentication server according to the configuration file information when authenticating users.
