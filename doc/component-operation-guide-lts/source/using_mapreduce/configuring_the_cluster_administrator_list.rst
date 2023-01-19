:original_name: mrs_01_0841.html

.. _mrs_01_0841:

Configuring the Cluster Administrator List
==========================================

Scenario
--------

This function is used to specify the MapReduce cluster administrator.

The system administrator list is specified by **mapreduce.cluster.administrators**. The cluster administrator **admin** has all operation permissions.

Configuration
-------------

On the **All Configurations** page of the MapReduce service, enter a parameter name in the search box. For details, see :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

.. table:: **Table 1** Parameter description

   +----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------+
   | Parameter                        | Description                                                                                                                                                                                                                                                                                                         | Default Value                              |
   +==================================+=====================================================================================================================================================================================================================================================================================================================+============================================+
   | mapreduce.cluster.acls.enabled   | Indicates whether to enable permission control on Job History Server.                                                                                                                                                                                                                                               | true                                       |
   +----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------+
   | mapreduce.cluster.administrators | Indicates the administrator list of the MapReduce cluster. You can configure both users and user groups. Multiple users or user groups are separated by commas (,), and users and user groups are separated by spaces, for example, userA,userB groupA,groupB. The value **\*** indicates all users or user groups. | mapred supergroup,System_administrator_186 |
   +----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+--------------------------------------------+
