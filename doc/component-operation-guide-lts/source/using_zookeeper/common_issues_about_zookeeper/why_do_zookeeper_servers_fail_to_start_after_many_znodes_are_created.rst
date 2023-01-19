:original_name: mrs_01_2108.html

.. _mrs_01_2108:

Why Do ZooKeeper Servers Fail to Start After Many znodes Are Created?
=====================================================================

Question
--------

After a large number of znodes are created, ZooKeeper servers in the ZooKeeper cluster become faulty and cannot be automatically recovered or restarted.

Logs of followers:

.. code-block::

   2016-06-23 08:00:18,763 | WARN  | QuorumPeer[myid=26](plain=/10.16.9.138:2181)(secure=disabled) | Exception when following the leader | org.apache.zookeeper.server.quorum.Follower.followLeader(Follower.java:93)
   java.net.SocketTimeoutException: Read timed out
       at java.net.SocketInputStream.socketRead0(Native Method)
       at java.net.SocketInputStream.socketRead(SocketInputStream.java:116)
       at java.net.SocketInputStream.read(SocketInputStream.java:170)
       at java.net.SocketInputStream.read(SocketInputStream.java:141)
       at java.io.BufferedInputStream.fill(BufferedInputStream.java:246)
       at java.io.BufferedInputStream.read(BufferedInputStream.java:265)
       at java.io.DataInputStream.readInt(DataInputStream.java:387)
       at org.apache.jute.BinaryInputArchive.readInt(BinaryInputArchive.java:63)
       at org.apache.zookeeper.server.quorum.QuorumPacket.deserialize(QuorumPacket.java:83)
       at org.apache.jute.BinaryInputArchive.readRecord(BinaryInputArchive.java:99)
       at org.apache.zookeeper.server.quorum.Learner.readPacket(Learner.java:156)
       at org.apache.zookeeper.server.quorum.Learner.registerWithLeader(Learner.java:276)
       at org.apache.zookeeper.server.quorum.Follower.followLeader(Follower.java:75)
       at org.apache.zookeeper.server.quorum.QuorumPeer.run(QuorumPeer.java:1094)

.. code-block::

   2016-06-23 08:00:18,764 | INFO  | QuorumPeer[myid=26](plain=/10.16.9.138:2181)(secure=disabled) | shutdown called | org.apache.zookeeper.server.quorum.Follower.shutdown(Follower.java:198)
   java.lang.Exception: shutdown Follower
       at org.apache.zookeeper.server.quorum.Follower.shutdown(Follower.java:198)
       at org.apache.zookeeper.server.quorum.QuorumPeer.stopFollower(QuorumPeer.java:1141)
       at org.apache.zookeeper.server.quorum.QuorumPeer.run(QuorumPeer.java:1098)

Logs of the leader:

.. code-block::

   2016-06-23 07:30:57,481 | WARN  | QuorumPeer[myid=25](plain=/10.16.9.136:2181)(secure=disabled) | Unexpected exception | org.apache.zookeeper.server.quorum.QuorumPeer.run(QuorumPeer.java:1108)
   java.lang.InterruptedException: Timeout while waiting for epoch to be acked by quorum
       at org.apache.zookeeper.server.quorum.Leader.waitForEpochAck(Leader.java:1221)
       at org.apache.zookeeper.server.quorum.Leader.lead(Leader.java:487)
       at org.apache.zookeeper.server.quorum.QuorumPeer.run(QuorumPeer.java:1105)

.. code-block::

   2016-06-23 07:30:57,482 | INFO  | QuorumPeer[myid=25](plain=/10.16.9.136:2181)(secure=disabled) | Shutdown called | org.apache.zookeeper.server.quorum.Leader.shutdown(Leader.java:623)
   java.lang.Exception: shutdown Leader! reason: Forcing shutdown
       at org.apache.zookeeper.server.quorum.Leader.shutdown(Leader.java:623)
       at org.apache.zookeeper.server.quorum.QuorumPeer.stopLeader(QuorumPeer.java:1149)
       at org.apache.zookeeper.server.quorum.QuorumPeer.run(QuorumPeer.java:1110)

Answer
------

After a large number of znodes are created, a large volume of data needs to be synchronized between the follower and leader. If the data synchronization is not complete within the specified time, all ZooKeeper servers fail to start.

Go to the **All Configurations** page of the ZooKeeper service by referring to :ref:`Modifying Cluster Service Configuration Parameters <mrs_01_1293>`. To recover ZooKeeper servers, increase the values of **syncLimit** and **initLimit** in the ZooKeeper configuration file **zoo.cfg** until ZooKeeper servers are successfully started.

.. table:: **Table 1** Parameters

   +-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | Parameter | Description                                                                                                                                                                                                                         | Default Value |
   +===========+=====================================================================================================================================================================================================================================+===============+
   | syncLimit | Interval (unit: tick) at which data is synchronized between the follower and the leader. If the leader does not respond to the follower within the specified time, the connection between the leader and follower cannot be set up. | 15            |
   +-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
   | initLimit | Interval (unit: tick) within which the connection and synchronization between the follower and leader must be completed.                                                                                                            | 15            |
   +-----------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

If ZooKeeper servers do not recover even after **initLimit** and **syncLimit** are set to **300** ticks, check that no other application is killing the ZooKeeper. For example, if the parameter value is **300** and the ticket duration is 2000 ms, the maximum synchronization duration is 600s (300 x 2000 ms).

There may exist the situation where an overwhelming amount of data is created in ZooKeeper and it takes long to synchronize data between the follower and the leader and to save data to the hard disk. This means that ZooKeeper needs to run for a long time. Ensure that no other monitoring application kills the ZooKeeper while ZooKeeper is running.
