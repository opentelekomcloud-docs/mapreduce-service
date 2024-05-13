:original_name: mrs_01_0352.html

.. _mrs_01_0352:

Downloading a User Authentication File
======================================

Scenario
--------

When a user develops big data applications and runs them in an MRS cluster that supports Kerberos authentication, the user needs to prepare a **Machine-machine** user authentication file for accessing the MRS cluster. The keytab file in the authentication file can be used for user authentication.

This section describes how to download a **Machine-machine** user authentication file and export the keytab file on Manager. This operation is supported only in clusters with Kerberos authentication enabled or common clusters with the EIP function enabled.

.. note::

   Before downloading a **Human-machine** user authentication file, change the password for the user on MRS Manager to make the initial password set by the administrator invalid. Otherwise, the exported keytab file cannot be used. For details, see :ref:`Changing the Password of an Operation User <mrs_01_0350>`.

   The operations described in this section apply only to clusters of versions earlier than MRS 3.x.

   For clusters of **MRS 3.\ x** or later, see :ref:`Exporting an Authentication Credential File <admin_guide_000145>`.

Procedure
---------

#. Access MRS Manager. For details, see :ref:`Accessing MRS Manager (MRS 2.x or Earlier) <mrs_01_0102>`.
#. On MRS Manager, click **System**.
#. In the **Permission** area, click **Manage User**.
#. In the row of a user for whom you want to export the keytab file, choose **More** > **Download authentication credential** to download the authentication file. After the file is automatically generated, save it to a specified path and keep it secure.
#. Open the authentication file with a decompression program.

   -  **user.keytab** indicates a user keytab file used for user authentication.
   -  **krb5.conf** indicates the configuration file of the authentication server. The application connects to the authentication server according to this configuration file information when authenticating users.
