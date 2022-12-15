:original_name: mrs_01_2025.html

.. _mrs_01_2025:

How to Assign a Parameter Value in a Spark Command?
===================================================

Question
--------

Is it possible to assign parameter values through Spark commands, in addition to through a user interface or a configuration file?

Answer
------

Spark configuration options can be defined either in a configuration file or in Spark commands.

To assign a parameter value, run the --conf command on a Spark client. The parameter value takes effect immediately after the command is run.

The command format is --conf + parameter name + parameter value. Example command:

--conf spark.eventQueue.size=50000
