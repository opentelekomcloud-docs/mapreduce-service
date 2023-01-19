:original_name: mrs_01_1669.html

.. _mrs_01_1669:

Configuring the Damaged Disk Volume
===================================

Scenario
--------

In the open source version, if multiple data storage volumes are configured for a DataNode, the DataNode stops providing services by default if one of the volumes is damaged. You can change the value of **dfs.datanode.failed.volumes.tolerated** to specify the number of damaged disk volumes that are allowed. If the number of damaged volumes does not exceed the threshold, DataNode continues to provide services.

Configuration Description
-------------------------

**Navigation path for setting parameters:**

Go to the **All Configurations** page of HDFS and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

.. table:: **Table 1** Parameter description

   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter                             | Description                                                                                                                                                                                                                                                                                                                                  | Default Value |
   +=======================================+==============================================================================================================================================================================================================================================================================================================================================+===============+
   | dfs.datanode.failed.volumes.tolerated | Specifies the number of damaged volumes that are allowed before the DataNode stops providing services. By default, there must be at least one valid volume. The value **-1** indicates that the minimum value of a valid volume is **1**. The value greater than or equal to **0** indicates the number of damaged volumes that are allowed. | -1            |
   +---------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
