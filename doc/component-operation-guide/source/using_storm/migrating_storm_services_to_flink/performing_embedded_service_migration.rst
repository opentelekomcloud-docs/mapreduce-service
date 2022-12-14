:original_name: mrs_01_1051.html

.. _mrs_01_1051:

Performing Embedded Service Migration
=====================================

Scenarios
---------

This section describes how to embed Storm code in DataStream of Flink in embedded migration mode. For example, the code of Spout or Bolt compiled using Storm API is embedded.

Procedure
---------

#. In Flink, perform embedded conversion to Spout and Bolt in the Storm topology to convert them to Flink operators. The following is an example of the code:

   .. code-block::

      //set up the execution environment
      final StreamExecutionEnvironment env = StreamExecutionEnvironment.getExecutionEnvironment();
      //get input data
      final DataStream<String> text = getTextDataStream(env);
      final DataStream<Tuple2<String, Integer>> counts = text
        //split up the lines in pairs (2-tuples) containing: (word,1)
        //this is done by a bolt that is wrapped accordingly
        .transform("CountBolt",
          TypeExtractor.getForObject(new Tuple2<String, Integer>("", 0)),
          new BoltWrapper<String, Tuple2<String, Integer>>(new CountBolt()))
        //group by the tuple field "0" and sum up tuple field "1"
        .keyBy(0).sum(1);
      // execute program
      env.execute("Streaming WordCount with bolt tokenizer");

#. After the modification, run the following command to submit the modification:

   **flink run -class {MainClass} WordCount.jar**
