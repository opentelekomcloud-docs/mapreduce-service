:original_name: mrs_01_1591.html

.. _mrs_01_1591:

Optimizing the Design of Partitioning Method
============================================

Scenarios
---------

The divide of tasks can be optimized by optimizing the partitioning method. If data skew occurs in a certain task, the whole execution process is delayed. Therefore, when designing the partitioning method, ensure that partitions are evenly assigned.

Procedure
---------

Partitioning methods are as follows:

-  **Random partitioning**: randomly partitions data.

   .. code-block::

      dataStream.shuffle();

-  **Rebalancing (round-robin partitioning)**: evenly partitions data based on round-robin. The partitioning method is useful to optimize data with data skew.

   .. code-block::

      dataStream.rebalance();

-  **Rescaling**: assign data to downstream subsets in the form of round-robin. The partitioning method is useful if you want to deliver data from each parallel instance of a data source to subsets of some mappers without the using rebalance (), that is, the complete rebalance operation.

   .. code-block::

      dataStream.rescale();

-  **Broadcast**: broadcast data to all partitions.

   .. code-block::

      dataStream.broadcast();

-  **User-defined partitioning**: use a user-defined partitioner to select a target task for each element. The user-defined partitioning allows user to partition data based on a certain feature to achieve optimized task execution.

   The following is an example:

   .. code-block::

      // fromElements builds simple Tuple2 stream
      DataStream<Tuple2<String, Integer>> dataStream = env.fromElements(Tuple2.of("hello",1), Tuple2.of("test",2), Tuple2.of("world",100));

      // Defines the key value used for partitioning. Adding one to the value equals to the id.
      Partitioner<Tuple2<String, Integer>> strPartitioner = new Partitioner<Tuple2<String, Integer>>() {
          @Override
          public int partition(Tuple2<String, Integer> key, int numPartitions) {
              return (key.f0.length() + key.f1) % numPartitions;
          }
      };

      // The Tuple2 data is used as the basis for partitioning.

      dataStream.partitionCustom(strPartitioner, new KeySelector<Tuple2<String, Integer>, Tuple2<String, Integer>>() {
          @Override
          public Tuple2<String, Integer> getKey(Tuple2<String, Integer> value) throws Exception {
              return value;
          }
      }).print();
