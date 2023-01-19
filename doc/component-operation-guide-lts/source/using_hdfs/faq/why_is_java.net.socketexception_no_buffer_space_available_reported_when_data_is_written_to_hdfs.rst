:original_name: mrs_01_1705.html

.. _mrs_01_1705:

Why Is "java.net.SocketException: No buffer space available" Reported When Data Is Written to HDFS
==================================================================================================

Question
--------

Why is an "java.net.SocketException: No buffer space available" exception reported when data is written to HDFS?

This problem occurs when files are written to the HDFS. Check the error logs of the client and DataNode.

The client logs are as follows:


.. figure:: /_static/images/en-us_image_0000001296219452.jpg
   :alt: **Figure 1** Client logs

   **Figure 1** Client logs

DataNode logs are as follows:

.. code-block::

   2017-07-24 20:43:39,269 | ERROR | DataXceiver for client DFSClient_NONMAPREDUCE_996005058_86
    at /192.168.164.155:40214 [Receiving block BP-1287143557-192.168.199.6-1500707719940:blk_1074269754_528941 with io weight 10] | DataNode{data=FSDataset{dirpath='[/srv/BigData/hadoop/data1/dn/current, /srv/BigData/hadoop/data2/dn/current, /srv/BigData/hadoop/data3/dn/current, /srv/BigData/hadoop/data4/dn/current, /srv/BigData/hadoop/data5/dn/current, /srv/BigData/hadoop/data6/dn/current, /srv/BigData/hadoop/data7/dn/current]'}, localName='192-168-164-155:9866', datanodeUuid='a013e29c-4e72-400c-bc7b-bbbf0799604c', xmitsInProgress=0}:Exception transfering block BP-1287143557-192.168.199.6-1500707719940:blk_1074269754_528941 to mirror 192.168.202.99:9866: java.net.SocketException: No buffer space available | DataXceiver.java:870
   2017-07-24 20:43:39,269 | INFO | DataXceiver for client DFSClient_NONMAPREDUCE_996005058_86
    at /192.168.164.155:40214 [Receiving block BP-1287143557-192.168.199.6-1500707719940:blk_1074269754_528941 with io weight 10] | opWriteBlock BP-1287143557-192.168.199.6-1500707719940:blk_1074269754_528941 received exception java.net.SocketException: No buffer space available | DataXceiver.java:933
   2017-07-24 20:43:39,270 | ERROR | DataXceiver for client DFSClient_NONMAPREDUCE_996005058_86
    at /192.168.164.155:40214 [Receiving block BP-1287143557-192.168.199.6-1500707719940:blk_1074269754_528941 with io weight 10] | 192-168-164-155:9866:DataXceiver error processing WRITE_BLOCK operation src: /192.168.164.155:40214 dst: /192.168.164.155:9866 | DataXceiver.java:304 java.net.SocketException: No buffer space available
    at sun.nio.ch.Net.connect0(Native Method)
    at sun.nio.ch.Net.connect(Net.java:454)
    at sun.nio.ch.Net.connect(Net.java:446)
    at sun.nio.ch.SocketChannelImpl.connect(SocketChannelImpl.java:648)
    at org.apache.hadoop.net.SocketIOWithTimeout.connect(SocketIOWithTimeout.java:192)
    at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:531)
    at org.apache.hadoop.net.NetUtils.connect(NetUtils.java:495)
    at org.apache.hadoop.hdfs.server.datanode.DataXceiver.writeBlock(DataXceiver.java:800)
    at org.apache.hadoop.hdfs.protocol.datatransfer.Receiver.opWriteBlock(Receiver.java:138)
    at org.apache.hadoop.hdfs.protocol.datatransfer.Receiver.processOp(Receiver.java:74)
    at org.apache.hadoop.hdfs.server.datanode.DataXceiver.run(DataXceiver.java:265)
    at java.lang.Thread.run(Thread.java:748)

Answer
------

The preceding problem may be caused by network memory exhaustion.

You can increase the threshold of the network device based on the actual scenario.

Example:

.. code-block:: console

   [root@xxxxx ~]# cat /proc/sys/net/ipv4/neigh/default/gc_thresh*
   128
   512
   1024
   [root@xxxxx ~]# echo 512 > /proc/sys/net/ipv4/neigh/default/gc_thresh1
   [root@xxxxx ~]# echo 2048 > /proc/sys/net/ipv4/neigh/default/gc_thresh2
   [root@xxxxx ~]# echo 4096 > /proc/sys/net/ipv4/neigh/default/gc_thresh3
   [root@xxxxx ~]# cat /proc/sys/net/ipv4/neigh/default/gc_thresh*
   512
   2048
   4096

You can also add the following parameters to the **/etc/sysctl.conf** file. The configuration takes effect even if the host is restarted.

.. code-block::

   net.ipv4.neigh.default.gc_thresh1 = 512
   net.ipv4.neigh.default.gc_thresh2 = 2048
   net.ipv4.neigh.default.gc_thresh3 = 4096
