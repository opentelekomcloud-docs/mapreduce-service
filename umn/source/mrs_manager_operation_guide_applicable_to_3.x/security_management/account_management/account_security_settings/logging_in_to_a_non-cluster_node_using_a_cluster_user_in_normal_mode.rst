:original_name: admin_guide_000248.html

.. _admin_guide_000248:

Logging In to a Non-Cluster Node Using a Cluster User in Normal Mode
====================================================================

Scenario
--------

When the cluster is installed in normal mode, the component clients do not support security authentication and cannot use the **kinit** command. Therefore, nodes outside the cluster cannot use users in the cluster by default. This may result in a user authentication failure when one of these nodes access a component server.

The node administrator can configure a user who has the same name as that of a user for a node outside the cluster, allow the user to log in to the node using the SSH protocol, and connect to the servers of components in the cluster by using the user who logs in to the OS.

Prerequisites
-------------

-  Nodes outside the cluster can connect to the service plane of the cluster.
-  The KrbServer service of the cluster is running properly.
-  You have obtained the password of user **root** of the node outside the cluster.
-  A human-machine user has been planned and added to the cluster, and you have obtained the authentication credential file. For details, see :ref:`Creating a User <admin_guide_000137>` and :ref:`Exporting an Authentication Credential File <admin_guide_000145>`.

Procedure
---------

#. Log in to the node where a user is to be added as user **root**.

#. Run the following command:

   **rpm -qa \| grep pam** and **rpm -qa\| grep krb5-client**

   The following RPM packages are displayed:

   .. code-block::

      pam_krb5-32bit-2.3.1-47.12.1
      pam-modules-32bit-11-1.22.1
      yast2-pam-2.17.3-0.5.211
      pam-32bit-1.1.5-0.10.17
      pam_mount-32bit-0.47-13.16.1
      pam-config-0.79-2.5.58
      pam_krb5-2.3.1-47.12.1
      pam-doc-1.1.5-0.10.17
      pam-modules-11-1.22.1
      pam_mount-0.47-13.16.1
      pam_ldap-184-147.20
      pam-1.1.5-0.10.17
      krb5-client-1.6.3

#. Check whether the RPM packages in the list are installed in the OS.

   -  If yes, go to :ref:`5 <admin_guide_000248__en-us_topic_0046736680_conf_kerb>`.
   -  If no, go to :ref:`4 <admin_guide_000248__en-us_topic_0046736680_inst_kerb>`.

#. .. _admin_guide_000248__en-us_topic_0046736680_inst_kerb:

   Obtain the lacked RPM packages from the OS image, upload the files to the current directory, and run the following command to install the RPM package:

   **rpm -ivh \*.rpm**

   .. note::

      The RPM packages to be installed may bring security risks. The risks that may be brought by the installation of these RPM packages must be taken into consideration during OS hardening.

   After the RPM packages are installed, go to :ref:`5 <admin_guide_000248__en-us_topic_0046736680_conf_kerb>`.

#. .. _admin_guide_000248__en-us_topic_0046736680_conf_kerb:

   Run the following command to configure Kerberos authentication on PAM:

   **pam-config --add --krb5**

   .. note::

      If you need to cancel Kerberos authentication and system user login on a non-cluster node, run the **pam-config --delete --krb5** command as user **root**.

#. Decompress the authentication credential file to obtain **krb5.conf**, use WinSCP to upload this configuration file to the **/etc** directory on the node outside the cluster, and run the following command to configure related permission to enable other users to access the file, such as permission **604**:

   **chmod 604 /etc/krb5.conf**

#. Run the following command in the connection session as user **root** to add the corresponding OS user to the human-machine user, and specify **root** as the primary group.

   The OS user password is the same as the initial password when the human-machine user is created on Manager.

   **useradd** *User name* **-m -d /home/admin_test -g root -s /bin/bash**

   For example, if the name of the human-machine user is **admin_test**, run the following command:

   **useradd admin_test -m -d /home/admin_test -g root -s /bin/bash**

   .. note::

      When you use the newly added OS user to log in to the node by using the SSH protocol for the first time, the system prompts that the password has expired after you enter the user password, and the system prompts that the password needs to be changed after you enter the user password again. You need to enter a new password that meets the password complexity requirements of both the node OS and the cluster.
