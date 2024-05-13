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

#. Locate the row that contains the user whose keytab file needs to be exported, choose **More** > **Download Authentication Credential**, specify the save path after the file is automatically generated, and keep the file properly.

   The authentication credential includes the **krb5.conf** file of the Kerberos service.

   After the authentication credential file is decompressed, you can obtain the following two files:

   -  The **krb5.conf** file contains the authentication service connection information.
   -  The **user.keytab** file contains user authentication information.
