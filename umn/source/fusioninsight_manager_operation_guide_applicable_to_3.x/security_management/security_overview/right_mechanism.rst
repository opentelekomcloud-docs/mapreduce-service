:original_name: admin_guide_000236.html

.. _admin_guide_000236:

Right Mechanism
===============

FusionInsight adopts the Lightweight Directory Access Protocol (LDAP) to store data of users and user groups. Information about role definitions is stored in the relational database and the mapping between roles and rights is saved in components.

FusionInsight uses Kerberos for unified authentication.

The verification process of user rights is as follows:

#. A client (a user terminal or FusionInsight component service) invokes the FusionInsight authentication interface.
#. FusionInsight uses the login username and password for Kerberos authentication.
#. If the authentication succeeds, the client sends a request for accessing the server (a FusionInsight component service).
#. The server finds the user group and role to which the login user belongs.
#. The server obtains all rights of the user group and the role.
#. The server checks whether the client has the right to access the resources it applies for.

**Example (RBAC):**

There are three files in HDFS, that is, fileA, fileB, and fileC.

-  roleA has read and write right for fileA, and roleB has the read right for fileB.
-  groupA is bound to roleA, and groupB is bound to roleB.
-  userA belongs to groupA and roleB, and userB belongs to groupB.

When userA successfully logs in to the system and accesses the HDFS:

#. HDFS obtains the role (roleB) to which userA is bound.
#. HDFS also obtains the role (roleA) to which the user group of userA is bound.
#. In this case, userA has all the rights of roleA and roleB.
#. As a result, userA has read and write rights for fileA, has the read right on fileB, and has no right for fileC.

Similarly, when userB successfully logs in to the system and accesses the HDFS:

#. userB only has the rights of roleB.
#. As a result, userB has the read right on fileB, and has no rights for fileA and fileC.
