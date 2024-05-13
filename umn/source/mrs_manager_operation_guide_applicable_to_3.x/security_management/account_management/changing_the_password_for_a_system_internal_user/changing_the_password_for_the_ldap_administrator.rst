:original_name: admin_guide_000256.html

.. _admin_guide_000256:

Changing the Password for the LDAP Administrator
================================================

Scenario
--------

It is recommended that the administrator periodically changes the passwords of LDAP administrator accounts **cn=krbkdc,ou=Users,dc=hadoop,dc=com** and **cn=krbadmin,ou=Users,dc=hadoop,dc=com** to improve the system O&M security.

Impact on the System
--------------------

-  You need to restart the KrbServer service after changing the password.

-  After the password is changed, check whether the LDAP administrator accounts **cn=krbkdc,ou=Users,dc=hadoop,dc=com** and **cn=krbadmin,ou=Users,dc=hadoop,dc=com** are locked, run the following command on the active management node of the cluster to check whether **krbkdc** is locked (the method for user **krbadmin** is similar):

   .. note::

      OLdap port number obtaining method:

      #. Log in to MRS Manager, choose **System** > **OMS** > **oldap** > **Modify Configuration**:
      #. The **LDAP Listening Port** parameter value is **oldap port**.

   **ldapsearch -H ldaps://**\ *OMS_FLOAT\_ IP address:OLdap port* **-LLL -x -D** **cn=krbkdc,ou=Users,dc=hadoop,dc=com -W -b cn=krbkdc,ou=Users,dc=hadoop,dc=com -e ppolicy**

   Enter the password of the LDAP administrator account **krbkdc**. If the following message is displayed, the account is locked. For details about how to unlock the account, see :ref:`Unlocking LDAP Users and Management Accounts <admin_guide_000245>`.

   .. code-block::

      ldap_bind: Invalid credentials (49); Account locked

Prerequisites
-------------

You have obtained the management node IP address.

Procedure
---------

#. Log in to the active management node as user **omm** with the IP address of the active management node.

#. Run the following command to go to the related directory:

   **cd ${BIGDATA_HOME}/om-server/om/meta-0.0.1-SNAPSHOT/kerberos/scripts**

#. Run the following command to change the password of the LDAP administrator account:

   **./okerberos_modpwd.sh**

   Enter the old password and then enter a new password twice.

   The password complexity requirements are as follows:

   -  The password contains 16 to 32 characters.
   -  The password contains at least three types of the following: uppercase letters, lowercase letters, digits, spaces, and special characters which can only be :literal:`\`~!@#$%^&*()-_=+|[{}];,<.>/?.`
   -  The password cannot be the same as the current password.

   If the following information is displayed, the password is changed successfully.

   .. code-block::

      Modify kerberos server password successfully.

#. Log in to MRS Manager, click **Cluster**, click the name of the desired cluster, and choose **Services** > **KrbServer**. On the displayed page, choose **More** > **Restart Service**.

   Enter the password and do not select **Restart upper-layer services**. Click **OK** to restart the KrbServer service.
