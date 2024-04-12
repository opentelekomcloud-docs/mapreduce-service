:original_name: mrs_01_1019.html

.. _mrs_01_1019:

Optimizing HBase JVM Parameters
===============================

Scenario
--------

When the number of clusters reaches a certain scale, the default settings of the Java virtual machine (JVM) cannot meet the cluster requirements. In this case, the cluster performance deteriorates or the clusters may be unavailable. Therefore, JVM parameters must be properly configured based on actual service conditions to improve the cluster performance.

Procedure
---------

**Navigation path for setting parameters:**

The JVM parameters related to the HBase role must be configured in the **hbase-env.sh** file in the **${BIGDATA_HOME}/FusionInsight_HD_*/install/FusionInsight-HBase-2.2.3/hbase/conf/** directory.

Each role has JVM parameter configuration variables, as shown in :ref:`Table 1 <mrs_01_1019__en-us_topic_0000001219350781_t2451c7af790c44cc8f895f6d4dc68b55>`.

.. _mrs_01_1019__en-us_topic_0000001219350781_t2451c7af790c44cc8f895f6d4dc68b55:

.. table:: **Table 1** HBase-related JVM parameter configuration variables

   +-------------------------+----------------------------------------------------------------+
   | Variable                | Affected Role                                                  |
   +=========================+================================================================+
   | HBASE_OPTS              | All roles of HBase                                             |
   +-------------------------+----------------------------------------------------------------+
   | SERVER_GC_OPTS          | All roles on the HBase server, such as Master and RegionServer |
   +-------------------------+----------------------------------------------------------------+
   | CLIENT_GC_OPTS          | Client process of HBase                                        |
   +-------------------------+----------------------------------------------------------------+
   | HBASE_MASTER_OPTS       | Master of HBase                                                |
   +-------------------------+----------------------------------------------------------------+
   | HBASE_REGIONSERVER_OPTS | RegionServer of HBase                                          |
   +-------------------------+----------------------------------------------------------------+
   | HBASE_THRIFT_OPTS       | Thrift of HBase                                                |
   +-------------------------+----------------------------------------------------------------+

**Configuration example:**

.. code-block::

   export HADOOP_NAMENODE_OPTS="-Dhadoop.security.logger=${HADOOP_SECURITY_LOGGER:-INFO,RFAS} -Dhdfs.audit.logger=${HDFS_AUDIT_LOGGER:-INFO,NullAppender} $HADOOP_NAMENODE_OPTS"
