:original_name: mrs_01_0467.html

.. _mrs_01_0467:

Introduction to Storage-Compute Decoupling
==========================================

In scenarios that require large storage capacity and elastic compute resources, MRS enables you to store data in OBS and use an MRS cluster for data computing only. In this way, storage and compute are separated.

.. note::

   In the big data decoupled storage-compute scenario, the OBS parallel file system must be used to configure a cluster. Using common object buckets will greatly affect the cluster performance.

Process of using the storage-compute decoupling function:

#. Configure a storage-compute decoupled cluster using either of the following methods (agency is recommended):

   -  Bind an agency of the ECS type to an MRS cluster to access OBS, preventing the AK/SK from being exposed in the configuration file. For details, see :ref:`Configuring a Storage-Compute Decoupled Cluster (Agency) <mrs_01_0768>`.
   -  Configure the AK/SK in an MRS cluster. The AK/SK will be exposed in the configuration file in plaintext. Exercise caution when performing this operation. For details, see :ref:`Configuring a Storage-Compute Decoupled Cluster (AK/SK) <mrs_01_0468>`.

#. Use the cluster.

   For details, see the following sections':

   -  :ref:`Interconnecting Flink with OBS <mrs_01_1288>`
   -  :ref:`Interconnecting Flume with OBS <en-us_topic_0000001349137409>`
   -  :ref:`Interconnecting HDFS with OBS <mrs_01_1292>`
   -  :ref:`Interconnecting Hive with OBS <mrs_01_1286>`
   -  :ref:`Interconnecting MapReduce with OBS <mrs_01_0617>`
   -  :ref:`Interconnecting Spark2x with OBS <mrs_01_1289>`
   -  :ref:`Interconnecting Sqoop with External Storage Systems <mrs_01_24294>`
