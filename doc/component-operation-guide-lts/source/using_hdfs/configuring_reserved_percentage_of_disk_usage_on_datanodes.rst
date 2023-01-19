:original_name: mrs_01_1675.html

.. _mrs_01_1675:

Configuring Reserved Percentage of Disk Usage on DataNodes
==========================================================

Scenario
--------

When the Yarn local directory and DataNode directory are on the same disk, the disk with larger capacity can run more tasks. Therefore, more intermediate data is stored in the Yarn local directory.

Currently, you can set **dfs.datanode.du.reserved** to configure the absolute value of the reserved disk space on DataNodes. A small value cannot meet the requirements of a disk with large capacity. However, configuring a large value for a disk with same capacity wastes a lot of disk space.

To avoid this problem, a new parameter **dfs.datanode.du.reserved.percentage** is introduced to configure the reserved percentage of the disk space.

.. note::

   -  If **dfs.datanode.du.reserved.percentage** and **dfs.datanode.du.reserved** are configured at the same time, the larger value of the reserved disk space calculated using the two parameters is used as the reserved space of the data nodes.
   -  You are advised to set **dfs.datanode.du.reserved** or **dfs.datanode.du.reserved.percentage** based on the actual disk space.

Configuration Description
-------------------------

Go to the **All Configurations** page of HDFS and enter a parameter name in the search box by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`.

.. table:: **Table 1** Parameter description

   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                           | Description                                                                                                                                          | Default Value         |
   +=====================================+======================================================================================================================================================+=======================+
   | dfs.datanode.du.reserved.percentage | Indicates the percentage of the reserved disk space on DataNodes. The DataNode permanently reserves the disk space calculated using this percentage. | 10                    |
   |                                     |                                                                                                                                                      |                       |
   |                                     | The value is an integer ranging from 0 to 100.                                                                                                       |                       |
   +-------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
