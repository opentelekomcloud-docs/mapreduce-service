:original_name: mrs_01_1692.html

.. _mrs_01_1692:

Why MapReduce Tasks Fails in the Environment with Multiple NameServices?
========================================================================

Question
--------

Why MapReduce or Yarn tasks using the viewFS function fail to be executed in the environment with multiple NameServices?

Answer
------

When viewFS is used, only directories mounted to viewFS can be accessed. Therefore, the most possible reason is that the configured path is not on the mount point of viewFS. Example:

.. code-block::

   <property>
   <name>fs.defaultFS</name>
   <value>viewfs://ClusterX/</value>
   </property>
   <property>
   <name>fs.viewfs.mounttable.ClusterX.link./folder1</name>
   <value>hdfs://NS1/folder1</value>
   </property>
   <property>
   <name>fs.viewfs.mounttable.ClusterX.link./folder2</name>
   <value>hdfs://NS2/folder2</value>
   </property>

In the MR configuration that depends on the HDFS, the mounted directory needs to be used.

**Incorrect example**:

.. code-block::

   <property>
   <name>yarn.app.mapreduce.am.staging-dir</name>
   <value>/tmp/hadoop-yarn/staging</value>
   </property>

The root directory (/) cannot be accessed in viewFS.

**Correct example**:

.. code-block::

   <property>
   <name>yarn.app.mapreduce.am.staging-dir</name>
   <value>/folder1/tmp/hadoop-yarn/staging</value>
   </property>
