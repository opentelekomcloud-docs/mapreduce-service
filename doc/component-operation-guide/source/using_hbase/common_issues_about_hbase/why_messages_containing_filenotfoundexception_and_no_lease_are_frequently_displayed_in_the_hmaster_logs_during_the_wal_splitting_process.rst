:original_name: mrs_01_1655.html

.. _mrs_01_1655:

Why Messages Containing FileNotFoundException and no lease Are Frequently Displayed in the HMaster Logs During the WAL Splitting Process?
=========================================================================================================================================

Question
--------

Why messages containing FileNotFoundException and no lease are frequently displayed in the HMaster logs during the WAL splitting process?

.. code-block::

   2017-06-10 09:50:27,586 | ERROR | split-log-closeStream-2 | Couldn't close log at hdfs://hacluster/hbase/data/default/largeT1/2b48346d087275fe751fc049334fda93/recovered.edits/0000000000000000000.temp | org.apache.hadoop.hbase.wal.WALSplitter$LogRecoveredEditsOutputSink$2.call(WALSplitter.java:1330)
   java.io.FileNotFoundException: No lease on /hbase/data/default/largeT1/2b48346d087275fe751fc049334fda93/recovered.edits/0000000000000000000.temp (inode 1092653): File does not exist. [Lease.  Holder: DFSClient_NONMAPREDUCE_1202985678_1, pendingcreates: 1936]
   ?at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkLease(FSNamesystem.java:3432)
   ?at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.analyzeFileState(FSNamesystem.java:3223)
   ?at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getNewBlockTargets(FSNamesystem.java:3057)
   ?at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getAdditionalBlock(FSNamesystem.java:3011)
   ?at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.addBlock(NameNodeRpcServer.java:842)
   ?at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.addBlock(ClientNamenodeProtocolServerSideTranslatorPB.java:526)
   ?at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
   ?at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:616)
   ?at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:973)
   ?at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2260)
   ?at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2256)
   ?at java.security.AccessController.doPrivileged(Native Method)
   ?at javax.security.auth.Subject.doAs(Subject.java:422)
   ?at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1769)
   ?at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2254)

   ?at sun.reflect.GeneratedConstructorAccessor40.newInstance(Unknown Source)
   ?at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
   ?at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
   ?at org.apache.hadoop.ipc.RemoteException.instantiateException(RemoteException.java:106)
   ?at org.apache.hadoop.ipc.RemoteException.unwrapRemoteException(RemoteException.java:73)
   ?at org.apache.hadoop.hdfs.DataStreamer.locateFollowingBlock(DataStreamer.java:1842)
   ?at org.apache.hadoop.hdfs.DataStreamer.nextBlockOutputStream(DataStreamer.java:1639)
   ?at org.apache.hadoop.hdfs.DataStreamer.run(DataStreamer.java:665)

Answer
------

During the WAL splitting process, the WAL splitting timeout period is specified by the **hbase.splitlog.manager.timeout** parameter. If the WAL splitting process fails to complete within the timeout period, the task is submitted again. Multiple WAL splitting tasks may be submitted during a specified period. If the **temp** file is deleted when one WAL splitting task completes, other tasks cannot find the file and the FileNotFoudException exception is reported. To avoid the problem, perform the following modifications:

The default value of **hbase.splitlog.manager.timeout** is 600,000 ms. The cluster specification is that each RegionServer has 2,000 to 3,000 regions. When the cluster is normal (HBase is normal and HDFS does not have a large number of read and write operations), you are advised to adjust this parameter based on the cluster specifications. If the actual specifications (the actual average number of regions on each RegionServer) are greater than the default specifications (the default average number of regions on each RegionServer, that is, 2,000), the adjustment solution is (actual specifications/default specifications) x Default time.

Set the **splitlog** parameter in the **hbase-site.xml** file on the server. :ref:`Table 1 <mrs_01_1655__td061a2527dd94860b0b6d9989d7fd9ee>` describes the parameter.

.. _mrs_01_1655__td061a2527dd94860b0b6d9989d7fd9ee:

.. table:: **Table 1** Description of the **splitlog** parameter

   +--------------------------------+----------------------------------------------------------------------------------------------+---------------+
   | Parameter                      | Description                                                                                  | Default Value |
   +================================+==============================================================================================+===============+
   | hbase.splitlog.manager.timeout | Timeout period for receiving worker response by the distributed SplitLog management program. | 600000        |
   +--------------------------------+----------------------------------------------------------------------------------------------+---------------+
