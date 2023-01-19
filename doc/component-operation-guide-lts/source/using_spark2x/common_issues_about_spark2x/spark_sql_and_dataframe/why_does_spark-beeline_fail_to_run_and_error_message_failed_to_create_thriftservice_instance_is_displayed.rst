:original_name: mrs_01_2047.html

.. _mrs_01_2047:

Why Does Spark-beeline Fail to Run and Error Message "Failed to create ThriftService instance" Is Displayed?
============================================================================================================

Question
--------

Why does "Failed to create ThriftService instance" occur when spark beeline fails to run?

Beeline logs are as follows:

.. code-block::

   Error: Failed to create ThriftService instance (state=,code=0)
   Beeline version 1.2.1.spark by Apache Hive
   [INFO] Unable to bind key for unsupported operation: backward-delete-word
   [INFO] Unable to bind key for unsupported operation: backward-delete-word
   [INFO] Unable to bind key for unsupported operation: down-history
   [INFO] Unable to bind key for unsupported operation: up-history
   [INFO] Unable to bind key for unsupported operation: up-history
   [INFO] Unable to bind key for unsupported operation: down-history
   [INFO] Unable to bind key for unsupported operation: up-history
   [INFO] Unable to bind key for unsupported operation: down-history
   [INFO] Unable to bind key for unsupported operation: up-history
   [INFO] Unable to bind key for unsupported operation: down-history
   [INFO] Unable to bind key for unsupported operation: up-history
   [INFO] Unable to bind key for unsupported operation: down-history
   beeline>

In addition, the "Timed out waiting for client to connect" error log is generated on the JDBCServer. The details are as follows:

.. code-block::

   2017-07-12 17:35:11,284 | INFO  | [main] | Will try to open client transport with JDBC Uri: jdbc:hive2://192.168.101.97:23040/default;principal=spark/hadoop.<System domain name>@<System domain name>;healthcheck=true;saslQop=auth-conf;auth=KERBEROS;user.principal=spark/hadoop.<System domain name>@<System domain name>;user.keytab=${BIGDATA_HOME}/FusionInsight_HD_8.1.2.2/install/FusionInsight-Spark-3.1.1/keytab/spark/JDBCServer/spark.keytab | org.apache.hive.jdbc.HiveConnection.openTransport(HiveConnection.java:317)
   2017-07-12 17:35:11,326 | INFO  | [HiveServer2-Handler-Pool: Thread-92] | Client protocol version: HIVE_CLI_SERVICE_PROTOCOL_V8 | org.apache.proxy.service.ThriftCLIProxyService.OpenSession(ThriftCLIProxyService.java:554)
   2017-07-12 17:35:49,790 | ERROR | [HiveServer2-Handler-Pool: Thread-113] | Timed out waiting for client to connect.
   Possible reasons include network issues, errors in remote driver or the cluster has no available resources, etc.
   Please check YARN or Spark driver's logs for further information. | org.apache.proxy.service.client.SparkClientImpl.<init>(SparkClientImpl.java:90)
   java.util.concurrent.ExecutionException: java.util.concurrent.TimeoutException: Timed out waiting for client connection.
    at io.netty.util.concurrent.AbstractFuture.get(AbstractFuture.java:37)
    at org.apache.proxy.service.client.SparkClientImpl.<init>(SparkClientImpl.java:87)
    at org.apache.proxy.service.client.SparkClientFactory.createClient(SparkClientFactory.java:79)
    at org.apache.proxy.service.SparkClientManager.createSparkClient(SparkClientManager.java:145)
    at org.apache.proxy.service.SparkClientManager.createThriftServerInstance(SparkClientManager.java:160)
    at org.apache.proxy.service.ThriftServiceManager.getOrCreateThriftServer(ThriftServiceManager.java:182)
    at org.apache.proxy.service.ThriftCLIProxyService.OpenSession(ThriftCLIProxyService.java:596)
    at org.apache.hive.service.cli.thrift.TCLIService$Processor$OpenSession.getResult(TCLIService.java:1257)
    at org.apache.hive.service.cli.thrift.TCLIService$Processor$OpenSession.getResult(TCLIService.java:1242)
    at org.apache.thrift.ProcessFunction.process(ProcessFunction.java:39)
    at org.apache.thrift.TBaseProcessor.process(TBaseProcessor.java:39)
    at org.apache.hadoop.hive.thrift.HadoopThriftAuthBridge$Server$TUGIAssumingProcessor.process(HadoopThriftAuthBridge.java:696)
    at org.apache.thrift.server.TThreadPoolServer$WorkerProcess.run(TThreadPoolServer.java:286)
    at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
    at java.lang.Thread.run(Thread.java:748)
   Caused by: java.util.concurrent.TimeoutException: Timed out waiting for client connection.

Answer
------

This problem occurs when the network is unstable. When a timed-out exception occurs in beeline, Spark does not attempt to reconnect to beeline. Therefore, you need to restart spark-beeline for reconnection.
