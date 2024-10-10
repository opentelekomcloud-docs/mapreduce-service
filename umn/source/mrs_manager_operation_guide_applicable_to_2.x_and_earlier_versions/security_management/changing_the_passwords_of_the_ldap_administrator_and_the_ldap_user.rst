:original_name: mrs_01_0565.html

.. _mrs_01_0565:

Changing the Passwords of the LDAP Administrator and the LDAP User
==================================================================

Scenario
--------

This section describes how to periodically change the passwords of the LDAP administrator **rootdn:cn=root,dc=hadoop,dc=com** and the LDAP user **pg_search_dn:cn=pg_search_dn,ou=Users,dc=hadoop,dc=com** to improve the system O&M security.

Impact on the System
--------------------

All services need to be restarted for the new password to take effect. The services are unavailable during the restart.

Procedure
---------

#. On MRS Manager, choose **Services > LdapServer > More**.

#. Click **Change Password**.

#. In the **Change Password** dialog box, select the user whose password needs to be modified in the **User Information** drop-down box.

#. Enter the old password in the **Old Password** text box, and enter the new password in the **New Password** and **Confirm Password** text boxes.

   The default password complexity requirements are as follows:

   -  The password contains 16 to 32 characters.
   -  The password must contain at least three types of the following: uppercase letters, lowercase letters, digits, and special characters :literal:`\`~!@#$%^&*()-_=+\\|[{}];:",<.>/?`.
   -  The password cannot be the username or the reverse username.
   -  The new password cannot be the same as the current password.

   .. note::

      The default password of the LDAP administrator **rootdn:cn=root,dc=hadoop,dc=com** is **LdapChangeMe@123**, and that of the LDAP user **pg_search_dn:cn=pg_search_dn,ou=Users,dc=hadoop,dc=com** is **pg_search_dn@123**. Periodically change the passwords and keep them secure.

#. Select **I have read the information and understand the impact**, and click **OK** to confirm the modification and restart the service.
