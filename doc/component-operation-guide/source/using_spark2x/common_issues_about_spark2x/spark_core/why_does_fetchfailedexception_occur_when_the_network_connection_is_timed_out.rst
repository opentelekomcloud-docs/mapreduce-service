:original_name: mrs_01_2007.html

.. _mrs_01_2007:

Why Does FetchFailedException Occur When the Network Connection Is Timed out
============================================================================

Question
--------

On a large cluster of 380 nodes, run the ScalaSort test case in the HiBench test that runs the 29T data, and configure Executor as **--executor-cores 4**. The following abnormality is displayed:

.. code-block::

   org.apache.spark.shuffle.FetchFailedException: Failed to connect to /192.168.114.12:23242
       at org.apache.spark.storage.ShuffleBlockFetcherIterator.throwFetchFailedException(ShuffleBlockFetcherIterator.scala:321)
       at org.apache.spark.storage.ShuffleBlockFetcherIterator.next(ShuffleBlockFetcherIterator.scala:306)
       at org.apache.spark.storage.ShuffleBlockFetcherIterator.next(ShuffleBlockFetcherIterator.scala:51)
       at scala.collection.Iterator$$anon$11.next(Iterator.scala:328)
       at scala.collection.Iterator$$anon$13.hasNext(Iterator.scala:371)
       at scala.collection.Iterator$$anon$11.hasNext(Iterator.scala:327)
       at org.apache.spark.util.CompletionIterator.hasNext(CompletionIterator.scala:32)
       at org.apache.spark.InterruptibleIterator.hasNext(InterruptibleIterator.scala:39)
       at org.apache.spark.util.collection.ExternalSorter.insertAll(ExternalSorter.scala:217)
       at org.apache.spark.shuffle.hash.HashShuffleReader.read(HashShuffleReader.scala:102)
       at org.apache.spark.rdd.ShuffledRDD.compute(ShuffledRDD.scala:90)
       at org.apache.spark.rdd.RDD.computeOrReadCheckpoint(RDD.scala:301)
       at org.apache.spark.rdd.RDD.iterator(RDD.scala:265)
       at org.apache.spark.rdd.MapPartitionsRDD.compute(MapPartitionsRDD.scala:38)
       at org.apache.spark.rdd.RDD.computeOrReadCheckpoint(RDD.scala:301)
       at org.apache.spark.rdd.RDD.iterator(RDD.scala:265)
       at org.apache.spark.rdd.MapPartitionsRDD.compute(MapPartitionsRDD.scala:38)
       at org.apache.spark.rdd.RDD.computeOrReadCheckpoint(RDD.scala:301)
       at org.apache.spark.rdd.RDD.iterator(RDD.scala:265)
       at org.apache.spark.rdd.UnionRDD.compute(UnionRDD.scala:87)
       at org.apache.spark.rdd.RDD.computeOrReadCheckpoint(RDD.scala:301)
       at org.apache.spark.rdd.RDD.iterator(RDD.scala:265)
       at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:73)
       at org.apache.spark.scheduler.ShuffleMapTask.runTask(ShuffleMapTask.scala:41)
       at org.apache.spark.scheduler.Task.run(Task.scala:87)
       at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:213)
       at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
       at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
       at java.lang.Thread.run(Thread.java:745)
   Caused by: java.io.IOException: Failed to connect to /192.168.114.12:23242
       at org.apache.spark.network.client.TransportClientFactory.createClient(TransportClientFactory.java:214)
       at org.apache.spark.network.client.TransportClientFactory.createClient(TransportClientFactory.java:167)
       at org.apache.spark.network.netty.NettyBlockTransferService$$anon$1.createAndStart(NettyBlockTransferService.scala:91)
       at org.apache.spark.network.shuffle.RetryingBlockFetcher.fetchAllOutstanding(RetryingBlockFetcher.java:140)
       at org.apache.spark.network.shuffle.RetryingBlockFetcher.access$200(RetryingBlockFetcher.java:43)
       at org.apache.spark.network.shuffle.RetryingBlockFetcher$1.run(RetryingBlockFetcher.java:170)
       at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
       at java.util.concurrent.FutureTask.run(FutureTask.java:266)
       ... 3 more
   Caused by: java.net.ConnectException: Connection timed out: /192.168.114.12:23242
       at sun.nio.ch.SocketChannelImpl.checkConnect(Native Method)
       at sun.nio.ch.SocketChannelImpl.finishConnect(SocketChannelImpl.java:717)
       at io.netty.channel.socket.nio.NioSocketChannel.doFinishConnect(NioSocketChannel.java:224)
       at io.netty.channel.nio.AbstractNioChannel$AbstractNioUnsafe.finishConnect(AbstractNioChannel.java:289)
       at io.netty.channel.nio.NioEventLoop.processSelectedKey(NioEventLoop.java:528)
       at io.netty.channel.nio.NioEventLoop.processSelectedKeysOptimized(NioEventLoop.java:468)
       at io.netty.channel.nio.NioEventLoop.processSelectedKeys(NioEventLoop.java:382)
       at io.netty.channel.nio.NioEventLoop.run(NioEventLoop.java:354)
       at io.netty.util.concurrent.SingleThreadEventExecutor$2.run(SingleThreadEventExecutor.java:111)
       ... 1 more

Answer
------

When an application is run, configure the Executor parameter as **--executor-cores 4**. The degree of parallelism (DOP) is high in a single process, resulting in that the IO is highly occupied and the task works slowly.

.. code-block::

   16/02/26 10:04:53 INFO TaskSetManager: Finished task 2139.0 in stage 1.0 (TID 151149) in 376455 ms on 10-196-115-2 (694/153378)

Because running a single task takes more than 6 minutes. The network connection is timed out and the running task fails.

Set the number of cores as 1, which is **--executor-cores 1**. A task is executed smoothly in proper time (within 15s).

.. code-block::

   16/02/29 02:24:46 INFO TaskSetManager: Finished task 59564.0 in stage 1.0 (TID 208574) in 15088 ms on 10-196-115-6 (59515/153378)

Therefore, to process the task of network connection timed out and avoid such error, you can reduce the core number of a single Executor.
