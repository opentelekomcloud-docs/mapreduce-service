:original_name: mrs_01_1722.html

.. _mrs_01_1722:

HetuEngine Permission Management Overview
=========================================

HetuEngine supports permission control for clusters in security mode. For clusters in non-security mode, permission control is not performed.

In security mode, HetuEngine provides two permission control modes: Ranger and MetaStore. The Ranger mode is used by default.

The following table lists the differences between Ranger and MetaStore. Both Ranger and MetaStore support user, user group, and role authentication.

.. table:: **Table 1** Differences between Ranger and MetaStore

   +-------------------------+------------------+-----------------------------------------------------------------+-----------------------------------------------------------------------------------+
   | Permission Control Mode | Permission Model | Supported Data Source                                           | Description                                                                       |
   +=========================+==================+=================================================================+===================================================================================+
   | Ranger                  | PBAC             | Hive, HBase, Elasticsearch, GaussDB, HetuEngine, and ClickHouse | Row filtering, column masking, and fine-grained permission control are supported. |
   +-------------------------+------------------+-----------------------------------------------------------------+-----------------------------------------------------------------------------------+
   | MetaStore               | RBAC             | Hive                                                            | ``-``                                                                             |
   +-------------------------+------------------+-----------------------------------------------------------------+-----------------------------------------------------------------------------------+
