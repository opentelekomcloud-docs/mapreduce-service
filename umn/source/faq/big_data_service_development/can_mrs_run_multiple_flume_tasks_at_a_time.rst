:original_name: mrs_03_1059.html

.. _mrs_03_1059:

Can MRS Run Multiple Flume Tasks at a Time?
===========================================

The Flume client supports multiple independent data flows. You can configure and link multiple sources, channels, and sinks in the **properties.properties** configuration file. These components can be linked to form multiple flows.

The following is an example of configuring two data flows in a configuration file:

.. code-block::

   server.sources = source1 source2
   server.sinks = sink1 sink2
   server.channels = channel1 channel2

   #dataflow1
   server.sources.source1.channels = channel1
   server.sinks.sink1.channel = channel1

   #dataflow2
   server.sources.source2.channels = channel2
   server.sinks.sink2.channel = channel2
