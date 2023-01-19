:original_name: mrs_01_1799.html

.. _mrs_01_1799:

MapReduce Job Failed in Multiple NameService Environment
========================================================

Question
--------

MapReduce or Yarn job fails in multiple nameService environment using viewFS.

Answer
------

When using viewFS only the mount directories are accessible, so the most possible cause is that the path configured is not in one of the mounted paths. For example:

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

For all the MR properties which depends on HDFS, should use the paths inside mount folders.

**Incorrect:**

.. code-block::

   <property>
   <name>yarn.app.mapreduce.am.staging-dir</name>
   <value>/tmp/hadoop-yarn/staging</value>
   </property>

As the root folder (/) is not accessible in viewFS.

**Correct:**

.. code-block::

   <property>
   <name>yarn.app.mapreduce.am.staging-dir</name>
   <value>/folder1/tmp/hadoop-yarn/staging</value>
   </property>
