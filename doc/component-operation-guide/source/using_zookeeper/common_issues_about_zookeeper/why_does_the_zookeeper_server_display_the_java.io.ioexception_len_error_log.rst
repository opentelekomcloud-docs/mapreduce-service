:original_name: mrs_01_2109.html

.. _mrs_01_2109:

Why Does the ZooKeeper Server Display the java.io.IOException: Len Error Log?
=============================================================================

Question
--------

After a large number of znodes are created in a parent directory, the ZooKeeper client will fail to fetch all child nodes of this parent directory in a single request.

Logs of client:

.. code-block::

   2017-07-11 13:17:19,610 [myid:] - WARN  [New I/O worker #3:ClientCnxnSocketNetty$ZKClientHandler@468] - Exception caught: [id: 0xb66cbb85, /10.18.97.97:49192 :> 10.18.97.97/10.18.97.97:2181] EXCEPTION: java.nio.channels.ClosedChannelException
   java.nio.channels.ClosedChannelException
   at org.jboss.netty.handler.ssl.SslHandler$6.run(SslHandler.java:1580)
   at org.jboss.netty.channel.socket.ChannelRunnableWrapper.run(ChannelRunnableWrapper.java:40)
   at org.jboss.netty.channel.socket.nio.AbstractNioWorker.executeInIoThread(AbstractNioWorker.java:71)
   at org.jboss.netty.channel.socket.nio.NioWorker.executeInIoThread(NioWorker.java:36)
   at org.jboss.netty.channel.socket.nio.AbstractNioWorker.executeInIoThread(AbstractNioWorker.java:57)
   at org.jboss.netty.channel.socket.nio.NioWorker.executeInIoThread(NioWorker.java:36)
   at org.jboss.netty.channel.socket.nio.AbstractNioChannelSink.execute(AbstractNioChannelSink.java:34)
   at org.jboss.netty.handler.ssl.SslHandler.channelClosed(SslHandler.java:1566)
   at org.jboss.netty.channel.Channels.fireChannelClosed(Channels.java:468
   at org.jboss.netty.channel.socket.nio.AbstractNioWorker.close(AbstractNioWorker.java:376)
   at org.jboss.netty.channel.socket.nio.NioWorker.read(NioWorker.java:93)
   at org.jboss.netty.channel.socket.nio.AbstractNioWorker.process(AbstractNioWorker.java:109)
   at org.jboss.netty.channel.socket.nio.AbstractNioSelector.run(AbstractNioSelector.java:312)
   at org.jboss.netty.channel.socket.nio.AbstractNioWorker.run(AbstractNioWorker.java:90)
   at org.jboss.netty.channel.socket.nio.NioWorker.run(NioWorker.java:178)
   at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
   at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
   at java.lang.Thread.run(Thread.java:745)

Logs of leader:

.. code-block::

   2017-07-11 13:17:33,043 [myid:1] - WARN  [New I/O worker #7:NettyServerCnxn@445] - Closing connection to /10.18.101.110:39856
   java.io.IOException: Len error 45
   at org.apache.zookeeper.server.NettyServerCnxn.receiveMessage(NettyServerCnxn.java:438)
   at org.apache.zookeeper.server.NettyServerCnxnFactory$CnxnChannelHandler.processMessage(NettyServerCnxnFactory.java:267)
   at org.apache.zookeeper.server.NettyServerCnxnFactory$CnxnChannelHandler.messageReceived(NettyServerCnxnFactory.java:187)
   at org.jboss.netty.channel.SimpleChannelHandler.handleUpstream(SimpleChannelHandler.java:88)
   at org.jboss.netty.channel.DefaultChannelPipeline.sendUpstream(DefaultChannelPipeline.java:564)
   at org.jboss.netty.channel.DefaultChannelPipeline.sendUpstream(DefaultChannelPipeline.java:559)
   at org.jboss.netty.channel.Channels.fireMessageReceived(Channels.java:268)
   at org.jboss.netty.channel.Channels.fireMessageReceived(Channels.java:255)
   at org.jboss.netty.channel.socket.nio.NioWorker.read(NioWorker.java:88)
   at org.jboss.netty.channel.socket.nio.AbstractNioWorker.process(AbstractNioWorker.java:109)
   at org.jboss.netty.channel.socket.nio.AbstractNioSelector.run(AbstractNioSelector.java:312)
   at org.jboss.netty.channel.socket.nio.AbstractNioWorker.run(AbstractNioWorker.java:90)
   at org.jboss.netty.channel.socket.nio.NioWorker.run(NioWorker.java:178)
   at org.jboss.netty.util.ThreadRenamingRunnable.run(ThreadRenamingRunnable.java:108)
   at org.jboss.netty.util.internal.DeadLockProofWorker$1.run(DeadLockProofWorker.java:42)
   at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
   at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
   at java.lang.Thread.run(Thread.java:745)

Answer
------

After a large number of znodes are created in a single parent directory and the client tries to fetch all the child znodes in a single request, the server will fail to return because the results exceed the data size that can be stored in a znode.

To avoid this problem, set **jute.maxbuffer** to a larger value based on the client application.

**jute.maxbuffer** can only be set to a Java system property without the Zookeeper prefix. To set **jute.maxbuffer** to *X*, set **Djute.maxbuffer** to *X* when starting the ZooKeeper client or the service.

For example, set the parameter to 4 MB: **-Djute.maxbuffer=0x400000**.

.. table:: **Table 1** Parameters

   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter             | Description                                                                                                                          | Default Value         |
   +=======================+======================================================================================================================================+=======================+
   | jute.maxbuffer        | Specifies the maximum length of data that can be stored in znode. The unit is byte. Default value: 0xfffff, which is less than 1 MB. | 0xfffff               |
   |                       |                                                                                                                                      |                       |
   |                       | .. note::                                                                                                                            |                       |
   |                       |                                                                                                                                      |                       |
   |                       |    If this option is changed, the system property must be set on all servers and clients, otherwise problems will arise.             |                       |
   +-----------------------+--------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
