:original_name: mrs_01_2019.html

.. _mrs_01_2019:

Why Does the Out of Memory Error Occur in NodeManager During the Execution of Spark Applications
================================================================================================

Question
--------

During the execution of Spark applications, if the YARN External Shuffle service is enabled and there are too many shuffle tasks, the **java.lang.OutofMemoryError: Direct buffer Memory** error occurs, indicating insufficient memory. The error log is as follows:

.. code-block::

   2016-12-06 02:01:00,768 | WARN  | shuffle-server-38 | Exception in connection from /192.168.101.95:53680 | TransportChannelHandler.java:79
   io.netty.handler.codec.DecoderException: java.lang.OutOfMemoryError: Direct buffer memory
           at io.netty.handler.codec.ByteToMessageDecoder.channelRead(ByteToMessageDecoder.java:153)
           at io.netty.channel.AbstractChannelHandlerContext.invokeChannelRead(AbstractChannelHandlerContext.java:333)
           at io.netty.channel.AbstractChannelHandlerContext.fireChannelRead(AbstractChannelHandlerContext.java:319)
           at io.netty.channel.DefaultChannelPipeline.fireChannelRead(DefaultChannelPipeline.java:787)
           at io.netty.channel.nio.AbstractNioByteChannel$NioByteUnsafe.read(AbstractNioByteChannel.java:130)
           at io.netty.channel.nio.NioEventLoop.processSelectedKey(NioEventLoop.java:511)
           at io.netty.channel.nio.NioEventLoop.processSelectedKeysOptimized(NioEventLoop.java:468)
           at io.netty.channel.nio.NioEventLoop.processSelectedKeys(NioEventLoop.java:382)
           at io.netty.channel.nio.NioEventLoop.run(NioEventLoop.java:354)
           at io.netty.util.concurrent.SingleThreadEventExecutor$2.run(SingleThreadEventExecutor.java:116)
           at java.lang.Thread.run(Thread.java:745)
   Caused by: java.lang.OutOfMemoryError: Direct buffer memory
           at java.nio.Bits.reserveMemory(Bits.java:693)
           at java.nio.DirectByteBuffer.<init>(DirectByteBuffer.java:123)
           at java.nio.ByteBuffer.allocateDirect(ByteBuffer.java:311)
           at io.netty.buffer.PoolArena$DirectArena.newChunk(PoolArena.java:434)
           at io.netty.buffer.PoolArena.allocateNormal(PoolArena.java:179)
           at io.netty.buffer.PoolArena.allocate(PoolArena.java:168)
           at io.netty.buffer.PoolArena.reallocate(PoolArena.java:277)
           at io.netty.buffer.PooledByteBuf.capacity(PooledByteBuf.java:108)
           at io.netty.buffer.AbstractByteBuf.ensureWritable(AbstractByteBuf.java:251)
           at io.netty.buffer.AbstractByteBuf.writeBytes(AbstractByteBuf.java:849)
           at io.netty.buffer.AbstractByteBuf.writeBytes(AbstractByteBuf.java:841)
           at io.netty.buffer.AbstractByteBuf.writeBytes(AbstractByteBuf.java:831)
           at io.netty.handler.codec.ByteToMessageDecoder.channelRead(ByteToMessageDecoder.java:146)
           ... 10 more

Answer
------

In the Shuffle Service of YARN, the number of started threads are twice of the number of available CPU cores. The default size of direct buffer memory is 128 MB. If there are too many shuffle tasks connected at the same time, the direct buffer memory allocated to each thread service is insufficient. For example, if there are 40 CPU cores and there are 80 threads started by the Shuffle Service of YARN, the direct buffer memory allocated to each thread is less than 2 MB.

To solve this problem, increase the directory buffer memory based on the number of CPU cores in NodeManager. For example, if there are 40 of CPU cores, increase the direct buffer memory to 512 MB, that is, configure the **GC_OPTS** parameter of NodeManager as follows:

-XX:MaxDirectMemorySize=512M

.. note::

   By default, **-XX:MaxDirectMemorySize** is not configured in the **GC_OPTS** parameter. To configure it, you need to add it to the **GC_OPTS** parameter as an custom option.

To configure the **GC_OPTS** parameter, log in to FusionInsight Manager, choose **Cluster >** *Name of the desired cluster* **> Services** > **Yarn** > **Configurations**, click **All Configurations**, and choose **NodeManager > System**, and then modify the **GC_OPTS** parameter.

.. table:: **Table 1** Parameter description

   ========= ==================================== =============
   Parameter Description                          Default Value
   ========= ==================================== =============
   GC_OPTS   The GC parameter of YARN NodeManger. 128M
   ========= ==================================== =============
