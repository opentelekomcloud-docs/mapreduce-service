:original_name: mrs_01_0625.html

.. _mrs_01_0625:

Why Does the LoadIncrementalHFiles Tool Fail to Be Executed and "Permission denied" Is Displayed When Nodes in a Cluster Are Used to Import Data in Batches?
============================================================================================================================================================

Question
--------

Why does the LoadIncrementalHFiles tool fail to be executed and "Permission denied" is displayed when a Linux user is manually created in a normal cluster and DataNode in the cluster is used to import data in batches?

.. code-block::

   2020-09-20 14:53:53,808 WARN  [main] shortcircuit.DomainSocketFactory: error creating DomainSocket
   java.net.ConnectException: connect(2) error: Permission denied when trying to connect to '/var/run/FusionInsight-HDFS/dn_socket'
       at org.apache.hadoop.net.unix.DomainSocket.connect0(Native Method)
       at org.apache.hadoop.net.unix.DomainSocket.connect(DomainSocket.java:256)
       at org.apache.hadoop.hdfs.shortcircuit.DomainSocketFactory.createSocket(DomainSocketFactory.java:168)
       at org.apache.hadoop.hdfs.client.impl.BlockReaderFactory.nextDomainPeer(BlockReaderFactory.java:804)
       at org.apache.hadoop.hdfs.client.impl.BlockReaderFactory.createShortCircuitReplicaInfo(BlockReaderFactory.java:526)
       at org.apache.hadoop.hdfs.shortcircuit.ShortCircuitCache.create(ShortCircuitCache.java:785)
       at org.apache.hadoop.hdfs.shortcircuit.ShortCircuitCache.fetchOrCreate(ShortCircuitCache.java:722)
       at org.apache.hadoop.hdfs.client.impl.BlockReaderFactory.getBlockReaderLocal(BlockReaderFactory.java:483)
       at org.apache.hadoop.hdfs.client.impl.BlockReaderFactory.build(BlockReaderFactory.java:360)
       at org.apache.hadoop.hdfs.DFSInputStream.getBlockReader(DFSInputStream.java:663)
       at org.apache.hadoop.hdfs.DFSInputStream.blockSeekTo(DFSInputStream.java:594)
       at org.apache.hadoop.hdfs.DFSInputStream.readWithStrategy(DFSInputStream.java:776)
       at org.apache.hadoop.hdfs.DFSInputStream.read(DFSInputStream.java:845)
       at java.io.DataInputStream.readFully(DataInputStream.java:195)
       at org.apache.hadoop.hbase.io.hfile.FixedFileTrailer.readFromStream(FixedFileTrailer.java:401)
       at org.apache.hadoop.hbase.io.hfile.HFile.isHFileFormat(HFile.java:651)
       at org.apache.hadoop.hbase.io.hfile.HFile.isHFileFormat(HFile.java:634)
       at org.apache.hadoop.hbase.tool.LoadIncrementalHFiles.visitBulkHFiles(LoadIncrementalHFiles.java:1090)
       at org.apache.hadoop.hbase.tool.LoadIncrementalHFiles.discoverLoadQueue(LoadIncrementalHFiles.java:1006)
       at org.apache.hadoop.hbase.tool.LoadIncrementalHFiles.prepareHFileQueue(LoadIncrementalHFiles.java:257)
       at org.apache.hadoop.hbase.tool.LoadIncrementalHFiles.doBulkLoad(LoadIncrementalHFiles.java:364)
       at org.apache.hadoop.hbase.tool.LoadIncrementalHFiles.run(LoadIncrementalHFiles.java:1263)
       at org.apache.hadoop.hbase.tool.LoadIncrementalHFiles.run(LoadIncrementalHFiles.java:1276)
       at org.apache.hadoop.hbase.tool.LoadIncrementalHFiles.run(LoadIncrementalHFiles.java:1311)
       at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
       at org.apache.hadoop.hbase.tool.LoadIncrementalHFiles.main(LoadIncrementalHFiles.java:1333)

Answer
------

If the client that the LoadIncrementalHFiles tool depends on is installed in the cluster and is on the same node as DataNode, HDFS creates short-circuit read during the execution of the tool to improve performance. The short-circuit read depends on the **/var/run/FusionInsight-HDFS** directory (**dfs.domain.socket.path**). The default permission on this directory is **750**. This user does not have the permission to operate the directory.

To solve the preceding problem, perform the following operations:

Method 1: Create a user (recommended).

#. Create a user on Manager. By default, the user group contains the **ficommon** group.

   .. code-block:: console

      [root@xxx-xxx-xxx-xxx ~]# id test
      uid=20038(test) gid=9998(ficommon) groups=9998(ficommon)

#. Import data again.

Method 2: Change the owner group of the current user.

#. Add the user to the **ficommon** group.

   .. code-block:: console

      [root@xxx-xxx-xxx-xxx ~]# usermod -a -G ficommon test
      [root@xxx-xxx-xxx-xxx ~]# id test
      uid=2102(test) gid=2102(test) groups=2102(test),9998(ficommon)

#. Import data again.
