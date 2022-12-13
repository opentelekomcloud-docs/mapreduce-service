:original_name: mrs_01_1579.html

.. _mrs_01_1579:

Security Features
=================

Security Features of Flink
--------------------------

-  All Flink cluster components support authentication.

   -  The Kerberos authentication is supported between Flink cluster components and external components, such as Yarn, HDFS, and ZooKeeper.
   -  The security cookie authentication between Flink cluster components, for example, Flink client and JobManager, JobManager and TaskManager, and TaskManager and TaskManager, are supported.

-  SSL encrypted transmission is supported by Flink cluster components.
-  SSL encrypted transmission between Flink cluster components, for example, Flink client and JobManager, JobManager and TaskManager, and TaskManager and TaskManager, are supported.
-  Following security hardening approaches for Flink web are supported:

   -  Whitelist filtering. Flink web can only be accessed through Yarn proxy.
   -  Security header enhancement.

-  In Flink clusters, ranges of listening ports of components can be configured.
-  In HA mode, ACL control is supported.
