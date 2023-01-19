:original_name: mrs_01_2026.html

.. _mrs_01_2026:

What Directory Permissions Do I Need to Create a Table Using SparkSQL?
======================================================================

Question
--------

The following error information is displayed when a new user creates a table using SparkSQL:

.. code-block::

   0: jdbc:hive2://192.168.169.84:22550/default> create table testACL(c string);
   Error: org.apache.spark.sql.execution.QueryExecutionException: FAILED: Execution Error, return code 1 from
   org.apache.hadoop.hive.ql.exec.DDLTask. MetaException(message:Got exception: org.apache.hadoop.security.AccessControlException
   Permission denied: user=testACL, access=EXECUTE, inode="/user/hive/warehouse/testacl":spark:hadoop:drwxrwx---
       at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkAccessAcl(FSPermissionChecker.java:403)
       at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.check(FSPermissionChecker.java:306)
       at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkTraverse(FSPermissionChecker.java:259)
       at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:205)
       at org.apache.hadoop.hdfs.server.namenode.FSPermissionChecker.checkPermission(FSPermissionChecker.java:190)
       at org.apache.hadoop.hdfs.server.namenode.FSDirectory.checkPermission(FSDirectory.java:1710)
       at org.apache.hadoop.hdfs.server.namenode.FSDirStatAndListingOp.getFileInfo(FSDirStatAndListingOp.java:109)
       at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.getFileInfo(FSNamesystem.java:3762)
       at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.getFileInfo(NameNodeRpcServer.java:1014)
       at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.getFileInfo(ClientNamenodeProtocolServerSideTranslatorPB.java:853)
       at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
       at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:616)
       at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:973)
       at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2089)
       at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2085)
       at java.security.AccessController.doPrivileged(Native Method)
       at javax.security.auth.Subject.doAs(Subject.java:422)
       at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1675)
       at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2083)
   ) (state=,code=0)

Answer
------

When you create a table using Spark SQL, the interface of Hive is called by the underlying system and a directory named after the table will be created in the **/user/hive/warehouse** directory. Therefore, you must have the permissions to read, write, and execute the **/user/hive/warehouse** directory or the group permission of Hive.

The\ **/user/hive/warehouse** is specified by the hive.metastore.warehouse.dir parameter.
