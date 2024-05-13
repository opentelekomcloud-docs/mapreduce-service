:original_name: admin_guide_000245.html

.. _admin_guide_000245:

Unlocking LDAP Users and Management Accounts
============================================

Scenario
--------

If the LDAP user **cn=pg_search_dn,ou=Users,dc=hadoop,dc=com** and LDAP management accounts **cn=krbkdc,ou=Users,dc=hadoop,dc=com** and **cn=krbadmin,ou=Users,dc=hadoop,dc=com** are locked, the administrator must unlock these accounts.

.. note::

   If you input an incorrect password for the LDAP user or management account for five consecutive times, the LDAP user or management account is locked. The account is automatically unlocked after 5 minutes.

Procedure
---------

#. Log in to the active management node as user **omm**.

#. Run the following command to go to the related directory:

   **cd ${BIGDATA_HOME}/om-server/om/ldapserver/ldapserver/local/script**

#. Run the following command to unlock the LDAP user or management account:

   **./ldapserver_unlockUsers.sh** *USER_NAME*

   In the command, *USER_NAME* indicates the name of the user to be unlocked.

   For example, to unlock the LDAP management **account cn=krbkdc,ou=Users,dc=hadoop,dc=com**, run the following command:

   **./ldapserver_unlockUsers.sh krbkdc**

   After the script is executed, enter the password of user **krbkdc** after **ROOT_DN_PASSWORD**. If the following information is displayed, the account is successfully unlocked.

   .. code-block::

      Unlock user krbkdc successfully.
