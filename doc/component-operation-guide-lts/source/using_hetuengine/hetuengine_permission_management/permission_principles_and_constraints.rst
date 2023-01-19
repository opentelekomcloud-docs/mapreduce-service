:original_name: mrs_01_1728.html

.. _mrs_01_1728:

Permission Principles and Constraints
=====================================

General Constraints
-------------------

-  Access data sources in the same cluster using HetuEngine

   If Ranger authentication is enabled for HetuEngine, the PBAC permission policy of Ranger is used for authentication.

   If Ranger authentication is disabled for HetuEngine, the RBAC permission policy of MetaStore is used for authentication.

-  Access data sources in different clusters using HetuEngine

   The permission policy is controlled by the permissions of the HetuEngine client and the data source. (In Hive scenarios, it depends on HDFS.)

-  HetuEngine users do not support the **supergroup** user group.

-  When querying a view, you only need to grant the select permission on the target view. When querying a join table using a view, you need to grant the select permission on the view and table.

.. note::

   When the permission control type of HetuEngine is changed, the HetuEngine service, including the HetuEngine compute instance running on Yarn, needs to be restarted.
