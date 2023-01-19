:original_name: mrs_01_1693.html

.. _mrs_01_1693:

DataNode Is Normal but Cannot Report Data Blocks
================================================

Question
--------

The DataNode is normal, but cannot report data blocks. As a result, the existing data blocks cannot be used.

Answer
------

This error may occur when the number of data blocks in a data directory exceeds four times the upper limit (4 x 1 MB). And the DataNode generates the following error logs:

.. code-block::

   2015-11-05 10:26:32,936 | ERROR | DataNode:[[[DISK]file:/srv/BigData/hadoop/data1/dn/]] heartbeating to
   vm-210/10.91.8.210:8020 | Exception in BPOfferService for Block pool BP-805114975-10.91.8.210-1446519981645
   (Datanode Uuid bcada350-0231-413b-bac0-8c65e906c1bb) service to vm-210/10.91.8.210:8020 | BPServiceActor.java:824
   java.lang.IllegalStateException:com.google.protobuf.InvalidProtocolBufferException:Protocol message was too large.May
   be malicious.Use CodedInputStream.setSizeLimit() to increase the size limit. at org.apache.hadoop.hdfs.protocol.BlockListAsLongs$BufferDecoder$1.next(BlockListAsLongs.java:369)
   at org.apache.hadoop.hdfs.protocol.BlockListAsLongs$BufferDecoder$1.next(BlockListAsLongs.java:347) at org.apache.hadoop.hdfs.
   protocol.BlockListAsLongs$BufferDecoder.getBlockListAsLongs(BlockListAsLongs.java:325) at org.apache.hadoop.hdfs.protocolPB.DatanodeProtocolClientSideTranslatorPB.
   blockReport(DatanodeProtocolClientSideTranslatorPB.java:190) at org.apache.hadoop.hdfs.server.datanode.BPServiceActor.blockReport(BPServiceActor.java:473)
   at org.apache.hadoop.hdfs.server.datanode.BPServiceActor.offerService(BPServiceActor.java:685) at org.apache.hadoop.hdfs.server.datanode.BPServiceActor.run(BPServiceActor.java:822)
   at java.lang.Thread.run(Thread.java:745) Caused by:com.google.protobuf.InvalidProtocolBufferException:Protocol message was too large.May be malicious.Use CodedInputStream.setSizeLimit()
   to increase the size limit. at com.google.protobuf.InvalidProtocolBufferException.sizeLimitExceeded(InvalidProtocolBufferException.java:110) at com.google.protobuf.CodedInputStream.refillBuffer(CodedInputStream.java:755)
   at com.google.protobuf.CodedInputStream.readRawByte(CodedInputStream.java:769) at com.google.protobuf.CodedInputStream.readRawVarint64(CodedInputStream.java:462) at com.google.protobuf.
   CodedInputStream.readSInt64(CodedInputStream.java:363) at org.apache.hadoop.hdfs.protocol.BlockListAsLongs$BufferDecoder$1.next(BlockListAsLongs.java:363)

The number of data blocks in the data directory is displayed as **Metric**. You can monitor its value through **http://<datanode-ip>:<http-port>/jmx**. If the value is greater than four times the upper limit (4 x 1 MB), you are advised to configure multiple drives and restart HDFS.

**Recovery procedure:**

#. Configure multiple data directories on the DataNode.

   For example, configure multiple directories on the DataNode where only the **/data1/datadir** directory is configured:

   .. code-block::

      <property> <name>dfs.datanode.data.dir</name> <value>/data1/datadir</value> </property>

   Configure as follows:

   .. code-block::

      <property> <name>dfs.datanode.data.dir</name> <value>/data1/datadir/,/data2/datadir,/data3/datadir</value> </property>

   .. note::

      You are advised to configure multiple data directories on multiple disks. Otherwise, performance may be affected.

#. Restart the HDFS.

#. Perform the following operation to move the data to the new data directory:

   **mv** */data1/datadir/current/finalized/subdir1 /data2/datadir/current/finalized/subdir1*

#. Restart the HDFS.
