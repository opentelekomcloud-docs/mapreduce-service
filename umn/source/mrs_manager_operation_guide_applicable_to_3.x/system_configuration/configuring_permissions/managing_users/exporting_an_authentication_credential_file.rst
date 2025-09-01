:original_name: admin_guide_000145.html

.. _admin_guide_000145:

Exporting an Authentication Credential File
===========================================

Scenario
--------

If a user uses a security mode cluster to develop applications, the keytab file of the user needs to be obtained for security authentication. You can export keytab files on MRS Manager.

.. note::

   After a user password is changed, the exported keytab file becomes invalid, and you need to export a keytab file again.

Prerequisites
-------------

Before downloading the keytab file of a Human-Machine user, the password of the user must be changed at least once on the Manager portal or a client; otherwise, the downloaded keytab file cannot be used For details, see :ref:`Changing a User Password <admin_guide_000143>`.

Procedure
---------

#. Log in to MRS Manager.

#. Choose **System** > **Permission** > **User**.

#. Locate the row that contains the target user, and choose **More** > **Download Authentication Credential**.

#. Select a location for downloading the authentication credential and set related parameters. This operation is supported only in MRS 3.5.0 and later versions.

   If the credential is downloaded to the server or a remote node, delete it after using it to prevent leakage.

   -  **Browser**: Download the file to the local computer.

   -  **Server**: Download the file to the active OMS node of the cluster.

      The generated file is stored in the **/tmp/FusionInsight-Keytab/** directory on the active OMS node by default. If the path does not exist, it will be created. If the path already has an authentication credential file, the existing authentication credential file will be overwritten. For user **omm**, write permission for the path is required.

      After the file is generated, copy the downloaded package to another directory as the **omm** user.

   -  **Remote node:** Download the file to a node other than the active OMS node. If you select this option, you need to set the following parameters:

      .. table:: **Table 1** Parameters

         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Parameter             | Description                                                                                                                              | Example Value                     |
         +=======================+==========================================================================================================================================+===================================+
         | Save to Path          | Path for storing the authentication credential file.                                                                                     | /tmp/FusionInsight-Keytab-Remote/ |
         |                       |                                                                                                                                          |                                   |
         |                       | If there is already a credential file in the path, it will be overwritten. For a remote node, write permission for the path is required. |                                   |
         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Host IP Address       | IP address of the remote node.                                                                                                           | x.x.x.x                           |
         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Host Port             | Host port of the remote node.                                                                                                            | 22                                |
         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Username              | Username for logging in to the remote node.                                                                                              | xxx                               |
         |                       |                                                                                                                                          |                                   |
         |                       | For a remote node, write permission for the path is required.                                                                            |                                   |
         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Authentication Method | You can choose one of the following methods:                                                                                             | Password                          |
         |                       |                                                                                                                                          |                                   |
         |                       | -  **Password**: Use the password for login.                                                                                             |                                   |
         |                       | -  **None**: To use this method, passwordless login needs to be enabled.                                                                 |                                   |
         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+
         | Password              | This parameter is mandatory when **Authentication Method** is set to **Password**.                                                       | xxx                               |
         |                       |                                                                                                                                          |                                   |
         |                       | This parameter indicates the password used for login.                                                                                    |                                   |
         +-----------------------+------------------------------------------------------------------------------------------------------------------------------------------+-----------------------------------+

#. Click **OK**. After the file is automatically generated, specify the save path and keep the file properly.

   The authentication credential includes the **krb5.conf** file of the Kerberos service.

   After the authentication credential file is decompressed, you can obtain the following two files:

   -  The **krb5.conf** file contains the authentication service connection information.
   -  The **user.keytab** file contains user authentication information.
