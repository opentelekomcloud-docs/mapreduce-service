:original_name: mrs_01_2097.html

.. _mrs_01_2097:

Configuring the ZooKeeper Permissions
=====================================

Scenario
--------

Configure znode permission of ZooKeeper.

ZooKeeper uses an access control list (ACL) to implement znode access control. The ZooKeeper client specifies a znode ACL, and the ZooKeeper server determines whether a client that requests for a znode has related operation permission according to the ACL. ACL configuration involves the following four operations:

-  Check znode ACLs in ZooKeeper.

-  Add znode ACLs to ZooKeeper.

-  Modify znode ACLs in ZooKeeper.

-  Delete znode ACLs from ZooKeeper.

   The ZooKeeper ACL permission is described as follows:

   ZooKeeper supports five types of permission, create, delete, read, write, and admin. ZooKeeper permission control is of a znode level. That is, the permission configuration for a parent znode is not inherited by its child znodes. The ZooKeeper znode default permission is **world:anyone: cdrwa**. That is, any user has all permissions.

.. note::

   ACL has three parts:

   The first part is the authentication type. For example, **world** indicates all authentication types and **sasl** indicates the kerberos authentication type.

   The second part is the account. For example, anyone indicates any user.

   The third part is permission. For example, **cdrwa** indicates all permissions.

   In particular, because starting the client in common mode does not need authentication, ACL with **sasl** authentication type cannot be used in common mode. Authentications of **sasl** scheme in this document are performed in clusters that have the security mode enabled.

.. table:: **Table 1** Five types of ZooKeeper ACLs

   +---------------------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | Permission Description    | Permission Name | Permission Details                                                                                                  |
   +===========================+=================+=====================================================================================================================+
   | Create permission         | create(c)       | Users with this permission can create child znodes in the current znode.                                            |
   +---------------------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | Delete permission         | delete(d)       | Users with this permission can delete the current znode.                                                            |
   +---------------------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | Read permission           | read(r)         | Users with this permission can obtain data of the current znode and list all the child znodes of the current znode. |
   +---------------------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | Write permission          | write(w)        | Users with this permission can write data to the current znode and its child znodes.                                |
   +---------------------------+-----------------+---------------------------------------------------------------------------------------------------------------------+
   | Administration permission | admin(a)        | Users with this permission can set permission for the current znode.                                                |
   +---------------------------+-----------------+---------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

.. important::

   Modifying ZooKeeper ACLs is a critical operation. If znode permission is modified in ZooKeeper, other users may have no permission to access the znode and some system functions are abnormal. In 3.5.6 and later versions, users must have the read permission for the **getAcl** operation.

Prerequisites
-------------

-  The ZooKeeper client has been installed. For example, the installation directory is **/opt/client**.
-  You have obtained the password of the system administrator account.

Procedure
---------

**Start the ZooKeeper client.**

#. Log in to the server where the ZooKeeper client is installed as user **root**.

#. Run the following command to go to the client installation directory:

   **cd /opt/client**

#. Run the following command to configure environment variables:

   **source bigdata_env**

#. If the cluster has the security mode enabled, run the following command for user authentication and enter the username and password (Any authorized user. **admin** is used as an example.):

   **kinit admin**

#. On the ZooKeeper client, run the following command to go to the ZooKeeper command-line interface (CLI):

   **sh zkCli.sh -server** *ZooKeeper* *plane IP address of any instance*:*clientPort*

   The default **clientPort** is **2181**.

   Example: **sh zkCli.sh -server 192.168.0.151:2181**

#. Run the **ls** command to view the znode list in ZooKeeper. For example, you can view the list of znodes in the root directory.

   **ls /**

   .. code-block::

      [zk: 192.168.0.151:2181(CONNECTED) 1] ls /
      [hadoop-flag, hadoop-ha, test, test2, test3, test4, test5, test6, zookeeper]

**View the ZooKeeper znode ACL.**

7. Start the ZooKeeper client.

8. Run the **getAcl** command to view znodes. The following command can be used to view the created znode ACL named **test**:

   **getAcl** /*znode name*

   .. code-block::

      [zk: 192.168.0.151:2181(CONNECTED) 2] getAcl /test
      'world,'anyone
      : cdrwa

Add a ZooKeeper znode ACL.

9.  Start the ZooKeeper client.

10. View the old ACL information to check whether the current account has the permission to modify the znode ACL information (a permission). If no, use kinit to switch to a user that has the permission and restart the ZooKeeper client.

    **getAcl** /*znode name*

    .. code-block::

        [zk: 192.168.0.151:2181(CONNECTED) 3] getAcl /test
       'world,'anyone
       : cdrwa

11. Run the **setAcl** command to add an ACL. The command for adding an ACL is as follows:

    **setAcl /test world:anyone:cdrwa,sasl:** *username*\ @: *<system domain name>*:*ACL value*

    For example, to add the ACL of the **admin** user to the test znode, run the following command:

    **setAcl /test world:anyone:cdrwa,sasl:admin@HADOOP.COM:cdrwa**

    .. note::

       When adding a new ACL, reserve the existing ones. The new and old ACLs are separated by a comma. The newly added ACL has three parts:

       The first part is the authentication type. For example, **sasl** indicates the kerberos authentication type.

       The second part is the account. For example, **admin@HADOOP.COM** indicates user **admin**.

       The third part is permission. For example, **cdrwa** indicates all permissions.

12. After adding the ACL, run the **getAcl** command to check whether the permission is added successfully:

    **getAcl** /*znode name*

    .. code-block::

       [zk: 192.168.0.151:2181(CONNECTED) 4] getAcl /test
       'world,'anyone
       : cdrwa
       'sasl,'admin@<system domain name>
       : cdrwa

**Modify the ZooKeeper znode ACL.**

13. Start the ZooKeeper client.

14. View the old ACL information to check whether the current account has the permission to modify the znode ACL information (a permission). If no, use kinit to switch to a user that has the permission and restart the ZooKeeper client.

    **getAcl** /*znode name*

    .. code-block::

       [zk: 192.168.0.151:2181(CONNECTED) 5] getAcl /test
       'world,'anyone
       : cdrwa
       'sasl,'admin@<system domain name>
       : cdrwa

15. Run the **setAcl** command to modify an ACL. The command for adding an ACL is as follows:

    s\ **etAcl /test sasl:**\ *Username@<System domain name>*:*ACL value*

    For example, to reserve only **admin** user permission and delete **anyone** rw permission, run the following command:

    **setAcl /test sasl:admin@HADOOP.COM:cdrwa**

16. After modifying the ACL, run the **getAcl** command to check whether the permission is modified successfully:

    **getAcl** /*znode name*

    .. code-block::

       [zk: 192.168.0.151:2181(CONNECTED) 6] getAcl /test
       'sasl,'admin@<system domain name>
       : cdrwa

**Delete the ZooKeeper znode ACL.**

17. Start the ZooKeeper client.

18. View the old ACL information to check whether the current account has the permission to modify the znode ACL information (a permission). If no, use kinit to switch to a user that has the permission and restart the ZooKeeper client.

    **getAcl** /*znode name*

    .. code-block::

       [zk: 192.168.0.151:2181(CONNECTED) 5] getAcl /test
       'world,'anyone
       : rw
       'sasl,'admin@<system domain name>
       : cdrwa

19. Run the **setAcl** command to add an ACL. The command for adding an ACL is as follows:

    s\ **etAcl /test sasl:**\ *Username@<System domain name>*:*ACL value*

    For example, to reserve only **admin** user permission and delete **anyone** rw permission, run the following command:

    **setAcl /test sasl:admin@HADOOP.COM:cdrwa**

20. After modifying the ACL, run the **getAcl** command to check whether the permission is modified successfully:

    **getAcl** /*znode name*

    .. code-block::

       [zk: 192.168.0.151:2181(CONNECTED) 6] getAcl /test
       'sasl,'admin@<system domain name>
       : cdrwa
