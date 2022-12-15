:original_name: mrs_01_1697.html

.. _mrs_01_1697:

Failed to Calculate the Capacity of a DataNode when Multiple data.dir Directories Are Configured in a Disk Partition
====================================================================================================================

Question
--------

The capacity of a DataNode fails to calculate when multiple data.dir directories are configured in a disk partition.

Answer
------

Currently, the capacity is calculated based on disks, which is similar to the **df** command in Linux. Ideally, users do not configure multiple data.dir directories in a disk partition. Otherwise, all data will be written to the same disk, greatly deteriorating the performance.

You are advised to configure them as below.

For example, if a node contains the following disks:

.. code-block::

   host-4:~ # df -h
   Filesystem      Size    Used    Avail    Use%   Mounted on
   /dev/sda1       352G   11G      324G    4%      /
   udev              190G    252K   190G    1%      /dev
   tmpfs             190G   72K      190G    1%     /dev/shm
   /dev/sdb1       2.7T    74G      2.5T      3%    /data1
   /dev/sdc1       2.7T    75G      2.5T      3%    /data2
   /dev/sdd1       2.7T    73G      2.5T      3%    /da

Recommended configuration:

.. code-block::

   <property>
   <name>dfs.datanode.data.dir</name>
   <value>/data1/datadir/,/data2/datadir,/data3/datadir</value>
   </property>

Unrecommended configuration:

.. code-block::

   <property>
   <name>dfs.datanode.data.dir</name>
   <value>/data1/datadir1/,/data2/datadir1,/data3/datadir1,/data1/datadir2,data1/datadir3,/data2/datadir2,/data2/datadir3,/data3/datadir2,/data3/datadir3</value>
   </property>
