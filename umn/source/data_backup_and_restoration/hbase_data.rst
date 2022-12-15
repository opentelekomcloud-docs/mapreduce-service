:original_name: mrs_01_0448.html

.. _mrs_01_0448:

HBase Data
==========

Currently, HBase data can be backed up in the following modes:

-  Snapshots
-  Replication
-  Export
-  CopyTable
-  HTable API
-  Offline backup of HDFS data

:ref:`Table 1 <mrs_01_0448__table163113513341>` compares the impact of operations from six perspectives.

.. _mrs_01_0448__table163113513341:

.. table:: **Table 1** Data backup mode comparison on HBase

   +-----------------------------+--------------------+----------------+--------------------------+--------------------+------------------------+----------------------------+
   | Backup Mode                 | Performance Impact | Data Footprint | Downtime                 | Incremental Backup | Ease of Implementation | Mean Time to Repair (MTTR) |
   +=============================+====================+================+==========================+====================+========================+============================+
   | Snapshots                   | Minimal            | Tiny           | Brief (Only for Restore) | No                 | Easy                   | Seconds                    |
   +-----------------------------+--------------------+----------------+--------------------------+--------------------+------------------------+----------------------------+
   | Replication                 | Minimal            | Large          | None                     | Intrinsic          | Medium                 | Seconds                    |
   +-----------------------------+--------------------+----------------+--------------------------+--------------------+------------------------+----------------------------+
   | Export                      | High               | Large          | None                     | Yes                | Easy                   | High                       |
   +-----------------------------+--------------------+----------------+--------------------------+--------------------+------------------------+----------------------------+
   | CopyTable                   | High               | Large          | None                     | Yes                | Easy                   | High                       |
   +-----------------------------+--------------------+----------------+--------------------------+--------------------+------------------------+----------------------------+
   | HTable API                  | Medium             | Large          | None                     | Yes                | Difficult              | Up to you                  |
   +-----------------------------+--------------------+----------------+--------------------------+--------------------+------------------------+----------------------------+
   | Offline backup of HDFS data | ``-``              | Large          | Long                     | No                 | Medium                 | High                       |
   +-----------------------------+--------------------+----------------+--------------------------+--------------------+------------------------+----------------------------+

Snapshots
---------

You can perform the snapshot operation on a table to generate a snapshot for the table. The snapshot can be used to back up the original table, roll back the original table when the original table is faulty, as well as back up data cross clusters. After a snapshot is executed, the **.hbase-snapshot** directory is generated in the HBase root directory (**/hbase** by default) on HBase. The directory contains details about each snapshot. When the **ExportSnapshot** command is executed to export the snapshot, an MR task is submitted locally to copy the snapshot information and table's **HFile** to **/hbase/.hbase-snapshot** and **/hbase/archive** of the standby cluster respectively. For details, see http://hbase.apache.org/2.2/book.html#ops.snapshots.

-  This backup mode has the following advantages:

   The single table backup efficiency is high. Online data can be backed up locally or remotely without interrupting services of the active and standby clusters. The number of maps and traffic threshold can be flexibly configured. A MapReduce executor node does not need to be deployed in the active and standby clusters. Therefore, no resource is consumed.

-  This backup mode has the following disadvantages and limitations:

   Only a single table can be backed up. The name of the table to be backed up has been specified in the snapshot and cannot be changed. Incremental backup cannot be performed. Resources are consumed when an MR task runs.

**Perform the following operations on the active cluster:**

#. Create a snapshot for a table. For example, create snapshot **member_snapshot** for the **member** table.

   **snapshot 'member','member_snapshot'**

#. Copy the snapshot to the standby cluster.

   **hbase org.apache.hadoop.hbase.snapshot.ExportSnapshot -snapshot member_snapshot -copy-to hdfs://IP address of the active NameNode of the HDFS service in the standby cluster:Port number/hbase -mappers 3**

   -  The data directory of the standby cluster must be the HBase root directory (**/hbase**).
   -  **mappers** indicates the number of maps to be submitted for an MR task.

**Perform the following operations on the standby cluster:**

Run the **restore** command to automatically create a table in the standby cluster and establish a link between HFile in **archive** and the table.

**restore_snapshot 'member_snapshot'**

.. note::

   If only table data needs to be backed up, Snapshots is highly recommended. Use SnapshotExport to submit an MR task locally and copies Snapshot and HFile to the standby cluster. Then, data can be directly loaded to the standby cluster, more efficient than using other methods.

Replication
-----------

In Replication backup mode, a disaster recovery relationship is established between the active and standby clusters on HBase. When data is written to the active cluster, the active cluster pushes data to the standby cluster through WAL to implement real-time data synchronization between the active and standby clusters. For details, see http://hbase.apache.org/2.2/book.html#_cluster_replication.

-  This backup mode has the following advantages:

   -  Replication is different from other data backup modes. After the active/standby relationship between clusters is established, data can be synchronized in real time without manual operations.
   -  The backup operation consumes few cluster resources and has little impact on cluster performance.
   -  Data synchronization reliability is high. If the standby cluster is stopped for a while and then recovered, data generated during this period on the active cluster can be still synchronized to the standby cluster.

-  This backup mode has the following disadvantages and limitations:

   -  If WAL is not set for data written by clients, data cannot be backed up to the standby cluster.
   -  The background synchronizes data in asynchronous mode, because only few resources can be occupied. Therefore, data is not synchronized in real time.
   -  If the data exists in the active cluster before you use the replication mode to perform synchronization, you need to use other methods to import these data to the standby cluster.
   -  If data is written to the active cluster in **bulkload** mode, it cannot be synchronized. (HBase on MRS enhances replication. Therefore, data written in the **bulkload** mode can be synchronized by replication.)

For details about how to use and configure HBase backup, see `Configuring HBase Replication <https://docs.otc.t-systems.com/cmpntguide/mrs/mrs_01_0501.html>`__ and `Using the ReplicationSyncUp Tool <https://docs.otc.t-systems.com/cmpntguide/mrs/mrs_01_0510.html>`__.

Export/Import
-------------

Export/Import starts a MapReduce task to scan the data table and writes SequenceFile to the remote HDFS. Then, Import reads SequenceFile and puts it on HBase.

-  This backup mode has the following advantages:

   Online copy does not interrupt services. Because data is written to new tables in **scan-** > **put** mode, Export/Import is more flexible than CopyTable. Data to be obtained and used flexibly, and written incrementally.

-  This backup mode has the following disadvantages and limitations:

   Export writes SequenceFiles to the remote HDFS through a MapReduce task, and then Import reads SequenceFiles and puts them on HBase. Therefore, an MR task needs to be executed twice, thus being inefficient.

**Perform the following operations on the active cluster:**

Run the **Export** command to export the table.

**hbase org.apache.hadoop.hbase.mapreduce.Export <tablename> <outputdir>**

Example: **hbase org.apache.hadoop.hbase.mapreduce.Export member hdfs://IP address of the active NameNode of the HDFS service in the standby cluster:Port number/user/table/member**

In the command, **member** indicates the name of the table to be exported.

**Perform the following operations on the standby cluster:**

#. After operations are executed on the active cluster, you can view the generated directory data on the standby cluster, as shown in :ref:`Figure 1 <mrs_01_0448__fig148041121174318>`.

   .. _mrs_01_0448__fig148041121174318:

   .. figure:: /_static/images/en-us_image_0000001349137569.png
      :alt: **Figure 1** Directory data

      **Figure 1** Directory data

#. Run the **create** command to create a table in the standby cluster with the same structure as that of the active cluster, for example, **member_import**.

#. .. _mrs_01_0448__li186481362121:

   Run the **Import** command to generate the HFile data on HDFS.

   **hbase org.apache.hadoop.hbase.mapreduce.Import <tablename> <inputdir>**

   Example: **hbase org.apache.hadoop.hbase.mapreduce.Import member_import /user/table/member -Dimport.bulk.output=/tmp/member**

   -  **member_import** indicates a table in the standby cluster with the same table structure as that of the active cluster.
   -  **Dimport.bulk.output** indicates the output directory of the HFile data.
   -  **/user/table/member** indicates the directory for storing data exported from the active cluster.

#. Perform the **Load** operation to write the HFile data to HBase.

   **hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /tmp/member member**

   -  **/tmp/member** indicates the output directory of the HFile data in :ref:`3 <mrs_01_0448__li186481362121>`.
   -  **member** indicates the name of the table to which data is to be imported in the standby cluster.

CopyTable
---------

The function of CopyTable is similar to that of Export. Like Export, CopyTable uses HBase API to create a MapReduce task to read data from the source table. However, the difference is that the output of CopyTable is an HBase table that can be stored in a local or remote cluster. For details, see http://hbase.apache.org/2.2/book.html#copy.table

-  This backup mode has the following advantages:

   The operation is simple. Online copy does not interrupt services. You can specify the **startrow**, **endrow**, and **timestamp** parameters of the backup data.

-  This backup mode has the following disadvantages and limitations:

   Only a single table can be operated. The efficiency is low when a large amount of data is remotely copied. The MapReduce task consumes local resources. The number of maps of the MapReduce task is determined by the number of regions in the table.

**Perform the following operations on the standby cluster:**

Run the **create** command to create a table in the standby cluster with the same structure as that of the active cluster, for example, **member_copy**.

**Perform the following operations on the active cluster:**

Run the following CopyTable command to copy the table:

**hbase org.apache.hadoop.hbase.mapreduce.CopyTable [--starttime=xxxxxx] [--endtime=xxxxxx] --new.name=member_copy --peer.adr=server1,server2,server3:2181:/hbase [--families=myOldCf:myNewCf,cf2,cf3] TestTable**

-  **starttime/endtime** indicates the timestamp of the data to be copied.
-  **new.name** indicates the name of the destination table in the standby cluster. The default name of the new table is the same as that of the original table.
-  **peer.adr** indicates the information about the ZooKeeper node in the standby cluster. The format is **quorumer:port:/hbase**.
-  **families** indicates the family column of the table to be copied.

.. note::

   If data is copied to a remote cluster, a MapReduce task is submitted on the host cluster to import the data. After the full or partial data in the original table is read, it is written to the remote cluster in **put** mode. Therefore, if the table contains a large amount of data (remote copy does not support **bulkload**), the efficiency is unsatisfactory.

HTable API
----------

HTable API imports and exports data of the original HBase table in the code. You can use the public API to write customized client applications to directly query tables, or design other methods based on the batch processing advantages of MapReduce tasks. This mode requires in-depth understanding of Hadoop development and the impact on the production cluster.

Offline backup of HDFS data
---------------------------

Offline backup of HDFS data means stopping the HBase service and allowing users to manually copy the HDFS data.

-  This backup mode has the following advantages:

   -  All data (including metadata) in the active cluster can be copied to the standby cluster at a time.
   -  Data is directly copied by DistCp. Therefore, the data backup efficiency is relatively high.

   -  You can copy data based on the site requirements. You can copy data of only one table or copy one HFile in a region.

-  This backup mode has the following disadvantages and limitations:

   -  This operation will overwrite the HDFS data directory in the standby cluster.
   -  If the HBase versions of the active and standby clusters are different, an error may occur when the HDFS directory is directly copied. For example, if the system table **index** is added to the MRS **hbase1.3** and overwritten by the HDFS directory of the earlier version, the table cannot be found. Therefore, exercise caution when using this mode.
   -  This operation has certain requirements on HBase capabilities. If an exception occurs, restore HBase based on the site requirements.

**Perform the following operations on the active cluster:**

#. Run the following command to save the data in the current cluster to HDFS permanently:

   **flush 'tableName'**

#. Stop the HBase service.

#. Run the following commands to copy the HDFS data of the current cluster to the standby cluster:

   **hadoop distcp -i /hbase/data hdfs://IP address of the active NameNode of the HDFS service in the standby cluster:Port number/hbase**

   **hadoop distcp -update -append -delete /hbase/ hdfs://IP address of the active NameNode of the HDFS service in the standby cluster:Port number/hbase/**

   The second command is used to incrementally copy files except the data directory. For example, data in **archive** may be referenced by the data directory.

**Perform the following operations on the standby cluster:**

#. Restart the HBase service for the data migration to take effect. During the restart, HBase loads the data in the current HDFS and regenerates metadata.

#. After the restart is complete, run the following command on the Master node client to load the HBase table data:

   .. code-block::

      $HBase_Home/bin/hbase hbck -fixMeta -fixAssignments

#. After the command is executed, run the following command repeatedly to check the health status of the HBase cluster until the health status is normal:

   .. code-block::

      hbase hbck

   .. note::

      If the HBase coprocessor is used and custom JAR files are stored in the **regionserver/hmaster** of the active cluster, you need to copy the custom JAR files before restarting the HBase service on the standby cluster.
