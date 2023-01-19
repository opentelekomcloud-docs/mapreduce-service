:original_name: mrs_01_1589.html

.. _mrs_01_1589:

Configuring DOP
===============

Scenario
--------

The degree of parallelism (DOP) indicates the number of tasks to be executed concurrently. It determines the number of data blocks after the operation. Configuring the DOP will optimize the number of tasks, data volume of each task, and the host processing capability.

Query the CPU and memory usage. If data and tasks are not evenly distributed among nodes, increase the DOP for even distribution.

Procedure
---------

Configure the DOP at one of the following layers (the priorities of which are in the descending order) based on the actual memory, CPU, data, and application logic conditions:

-  Operator

   Call the **setParallelism()** method to specify the DOP of an operator, data source, and sink. For example:

   .. code-block::

      final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();

      DataStream<String> text = [...]
      DataStream<Tuple2<String, Integer>> wordCounts = text
          .flatMap(new LineSplitter())
          .keyBy(0)
          .timeWindow(Time.seconds(5))
          .sum(1).setParallelism(5);

      wordCounts.print();

      env.execute("Word Count Example");

-  Execution environment

   Flink runs in the execution environment which defines a default DOP for operators, data source and data sink.

   Call the **setParallelism()** method to specify the default DOP of the execution environment. Example:

   .. code-block::

      final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
      env.setParallelism(3);
      DataStream<String> text = [...]
      DataStream<Tuple2<String, Integer>> wordCounts = [...]
      wordCounts.print();
      env.execute("Word Count Example");

-  Client

   Specify the DOP when submitting jobs to Flink on the client. If you use the CLI client, specify the DOP using the **-p** parameter. Example:

   .. code-block::

      ./bin/flink run -p 10 ../examples/*WordCount-java*.jar

-  System

   On the Flink client, modify the **parallelism.default** parameter in the **flink-conf.yaml** file under the conf to specify the DOP for all execution environments.
