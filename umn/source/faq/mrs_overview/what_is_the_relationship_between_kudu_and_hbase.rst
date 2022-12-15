:original_name: mrs_03_1066.html

.. _mrs_03_1066:

What Is the Relationship Between Kudu and HBase?
================================================

Kudu is designed based on the HBase structure and can implement fast random read/write and update functions that HBase is good at. Kudu and HBase are similar in architecture. The differences are as follows:

-  HBase uses ZooKeeper to ensure data consistency, whereas Kudu uses the Raft consensus algorithm to ensure consistency.
-  HBase uses HDFS for resilient data storage, whereas Kudu uses TServer to ensure strong data consistency and reliability.
