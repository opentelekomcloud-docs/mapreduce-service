:original_name: mrs_08_0039.html

.. _mrs_08_0039:

Kudu
====

Kudu is a column-store manager developed for the Apache Hadoop platform. Kudu shares the common technical properties of Hadoop ecosystem applications, that is, it runs on commodity hardware, which is horizontally scalable, delivering high availability.

Kudu's design has the following benefits:

-  Fast processing of OLAP workloads
-  Integration with MapReduce, Spark and other Hadoop ecosystem components
-  Tight integration with Apache Impala, making it a good, mutable alternative to using HDFS with Apache Parquet
-  Strong but flexible consistency model, allowing you to choose consistency requirements on a per-request basis, including the option for strict-serializable consistency
-  Strong performance for running sequential and random workloads simultaneously
-  Easy to manage
-  High availability Tablet Servers and Masters use the Raft Consensus Algorithm, which ensures that as long as more than half the total number of replicas is available, the tablet is available for reads and writes. For example, if 2 out of 3 replicas or 3 out of 5 replicas are available, the tablet is available. Reads can be serviced by read-only follower tablets, even in the event of a leader tablet failure.
-  Structured data model

By combining all of these properties, Kudu targets support for families of applications that are difficult or impossible to implement on current generation Hadoop storage technologies.

A few examples of applications for which Kudu is a great solution are:

-  Reporting applications where newly-arrived data needs to be immediately available for end users
-  Time-series applications that must simultaneously support queries across large amounts of historic data and granular queries about an individual entity that must return very quickly
-  Applications that use predictive models to make real-time decisions with periodic refreshes of the predictive model based on all historic data

Relationships with other components
-----------------------------------

-  HBase

   Kudu is designed based on the HBase structure and can implement fast random read/write and update functions that HBase features.

   The differences are as follows:

   -  HBase uses ZooKeeper to ensure data consistency, whereas Kudu uses the Raft consensus algorithm to ensure consistency.
   -  HBase uses HDFS for resilient data storage, whereas Kudu uses TServer to ensure strong data consistency and reliability.
