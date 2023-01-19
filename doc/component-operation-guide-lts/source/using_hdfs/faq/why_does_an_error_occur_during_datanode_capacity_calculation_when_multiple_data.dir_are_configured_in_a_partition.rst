:original_name: mrs_01_1697.html

.. _mrs_01_1697:

Why Does an Error Occur During DataNode Capacity Calculation When Multiple data.dir Are Configured in a Partition?
==================================================================================================================

Question
--------

DataNode capacity count incorrect if several data.dir configured in one disk partition.

Answer
------

Currently calculation will be done based on the disk like **df** command in linux. Ideally user should not configure multiple directories for same disk which will be huge impact on performance where all data will go to one disk.

Hence it is always better to configure like below:

For example:

if the machine is having disks like following:

.. code-block::

   host-4:~ # df -h
   Filesystem      Size    Used    Avail    Use%   Mounted on
   /dev/sda1       352G   11G      324G    4%      /
   udev              190G    252K   190G    1%      /dev
   tmpfs             190G   72K      190G    1%     /dev/shm
   /dev/sdb1       2.7T    74G      2.5T      3%    /data1
   /dev/sdc1       2.7T    75G      2.5T      3%    /data2
   /dev/sdd1       2.7T    73G      2.5T      3%    /data

Suggested way of configuration:

.. code-block::

   <property>
   <name>dfs.datanode.data.dir</name>
   <value>/data1/datadir/,/data2/datadir,/data3/datadir</value>
   </property>

Following is not recommended:

.. code-block::

   <property>
   <name>dfs.datanode.data.dir</name>
   <value>/data1/datadir1/,/data2/datadir1,/data3/datadir1,/data1/datadir2/data1/datadir3,/data2/datadir2,/data2/datadir3,/data3/datadir2,/data3/datadir3</value>
   </property>
