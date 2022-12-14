:original_name: mrs_01_2113.html

.. _mrs_01_2113:

What Should I Do When the ZooKeeper Client Fails to Refresh a TGT?
==================================================================

Question
--------

The ZooKeeper client fails to refresh a TGT and therefore ZooKeeper cannot be accessed. The error message is as follows:

.. code-block::

   Login: Could not renew TGT due to problem running shell command: '***/kinit -R'; exception was:org.apache.zookeeper.Shell$ExitCodeException: kinit: Ticket expired while renewing credentials

Answer
------

ZooKeeper uses the system command **kinit - R** to refresh a ticket. In the current version of MRS, the function of this command is canceled. If a long-term task needs to be executed, you are advised to implement the authentication function in keytab mode.

In the **jaas.conf** configuration file, set **useTicketCache** to **false**, **useKeyTab** to **true**, and specify the keytab path.
