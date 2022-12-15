:original_name: mrs_01_2212.html

.. _mrs_01_2212:

Why a Message Is Displayed Indicating that the Permission is Insufficient When CTBase Connects to the Ranger Plug-ins?
======================================================================================================================

Question
--------

When CTBase accesses the HBase service with the Ranger plug-ins enabled and you are creating a cluster table, a message is displayed indicating that the permission is insufficient.

.. code-block::

   ERROR: Create ClusterTable failed. Error: org.apache.hadoop.hbase.security.AccessDeniedException: Insufficient permissions for user 'ctbase2@HADOOP.COM' (action=create)
   at org.apache.ranger.authorization.hbase.AuthorizationSession.publishResults(AuthorizationSession.java:278)
   at org.apache.ranger.authorization.hbase.RangerAuthorizationCoprocessor.authorizeAccess(RangerAuthorizationCoprocessor.java:654)
   at org.apache.ranger.authorization.hbase.RangerAuthorizationCoprocessor.requirePermission(RangerAuthorizationCoprocessor.java:772)
   at org.apache.ranger.authorization.hbase.RangerAuthorizationCoprocessor.preCreateTable(RangerAuthorizationCoprocessor.java:943)
   at org.apache.ranger.authorization.hbase.RangerAuthorizationCoprocessor.preCreateTable(RangerAuthorizationCoprocessor.java:428)
   at org.apache.hadoop.hbase.master.MasterCoprocessorHost$12.call(MasterCoprocessorHost.java:351)
   at org.apache.hadoop.hbase.master.MasterCoprocessorHost$12.call(MasterCoprocessorHost.java:348)
   at org.apache.hadoop.hbase.coprocessor.CoprocessorHost$ObserverOperationWithoutResult.callObserver(CoprocessorHost.java:581)
   at org.apache.hadoop.hbase.coprocessor.CoprocessorHost.execOperation(CoprocessorHost.java:655)
   at org.apache.hadoop.hbase.master.MasterCoprocessorHost.preCreateTable(MasterCoprocessorHost.java:348)
   at org.apache.hadoop.hbase.master.HMaster$5.run(HMaster.java:2192)
   at org.apache.hadoop.hbase.master.procedure.MasterProcedureUtil.submitProcedure(MasterProcedureUtil.java:134)
   at org.apache.hadoop.hbase.master.HMaster.createTable(HMaster.java:2189)
   at org.apache.hadoop.hbase.master.MasterRpcServices.createTable(MasterRpcServices.java:711)
   at org.apache.hadoop.hbase.shaded.protobuf.generated.MasterProtos$MasterService$2.callBlockingMethod(MasterProtos.java)
   at org.apache.hadoop.hbase.ipc.RpcServer.call(RpcServer.java:458)
   at org.apache.hadoop.hbase.ipc.CallRunner.run(CallRunner.java:133)
   at org.apache.hadoop.hbase.ipc.RpcExecutor$Handler.run(RpcExecutor.java:338)
   at org.apache.hadoop.hbase.ipc.RpcExecutor$Handler.run(RpcExecutor.java:318)

Answer
------

CTBase users can configure permission policies on the Ranger page and grant the READ, WRITE, CREATE, ADMIN, and EXECUTE permissions to the CTBase metadata table **\_ctmeta\_**, cluster table, and index table.
