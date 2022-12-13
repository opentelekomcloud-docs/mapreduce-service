:original_name: mrs_01_1009.html

.. _mrs_01_1009:

Configuring Secure HBase Replication
====================================

Scenario
--------

This topic provides the procedure to configure the secure HBase replication during cross-realm Kerberos setup in security mode.

Prerequisites
-------------

-  Mapping for all the FQDNs to their realms should be defined in the Kerberos configuration file.
-  The passwords and keytab files of **ONE.COM** and **TWO.COM** must be the same.

Procedure
---------

#. Create krbtgt principals for the two realms.

   For example, if you have two realms called **ONE.COM** and **TWO.COM**, you need to add the following principals: **krbtgt/ONE.COM@TWO.COM** and **krbtgt/TWO.COM@ONE.COM**.

   Add these two principals at both realms.

   .. code-block::

      kadmin: addprinc -e "<enc_type_list>" krbtgt/ONE.COM@TWO.COM
      kadmin: addprinc -e "<enc_type_list>" krbtgt/TWO.COM@ONE.COM

   .. note::

      There must be at least one common keytab mode between these two realms.

#. Add rules for creating short names in Zookeeper.

   **Dzookeeper.security.auth_to_local** is a parameter of the ZooKeeper server process. Following is an example rule that illustrates how to add support for the realm called **ONE.COM**. The principal has two members (such as **service/instance@ONE.COM**).

   .. code-block::

      Dzookeeper.security.auth_to_local=RULE:[2:\$1@\$0](.*@\\QONE.COM\\E$)s/@\\QONE.COM\\E$//DEFAULT

   The above code example adds support for the **ONE.COM** realm in a different realm. Therefore, in the case of replication, you must add a rule for the master cluster realm in the slave cluster realm. **DEFAULT** is for defining the default rule.

#. Add rules for creating short names in the Hadoop processes.

   The following is the **hadoop.security.auth_to_local** property in the **core-site.xml** file in the slave cluster HBase processes. For example, to add support for the **ONE.COM** realm:

   .. code-block::

      <property>
      <name>hadoop.security.auth_to_local</name>
      <value>RULE:[2:$1@$0](.*@\QONE.COM\E$)s/@\QONE.COM\E$//DEFAULT</value>
      </property>

   .. note::

      If replication for bulkload data is enabled, then the same property for supporting the slave realm needs to be added in the **core-site.xml** file in the master cluster HBase processes.

      Example:

      .. code-block::

         <property>
         <name>hadoop.security.auth_to_local</name>
         <value>RULE:[2:$1@$0](.*@\QTWO.COM\E$)s/@\QTWO.COM\E$//DEFAULT</value>
         </property>
