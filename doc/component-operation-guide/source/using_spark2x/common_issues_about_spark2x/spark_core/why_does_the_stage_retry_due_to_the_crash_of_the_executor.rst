:original_name: mrs_01_2017.html

.. _mrs_01_2017:

Why Does the Stage Retry due to the Crash of the Executor?
==========================================================

Question
--------

When I run Spark tasks with a large data volume, for example, 100 TB TPCDS test suite, why does the Stage retry due to Executor loss sometimes? The message "Executor 532 is lost rpc with driver, but is still alive, going to kill it" is displayed, indicating that the loss of the Executor is caused by a JVM crash.

The log of the key JVM crash is as follows:

.. code-block::

   #
   # A fatal error has been detected by the Java Runtime Environment:
   #
   #  Internal Error (sharedRuntime.cpp:834), pid=241075, tid=140476258551552
   #  fatal error: exception happened outside interpreter, nmethods and vtable stubs at pc 0x00007fcda9eb8eb1

Answer
------

This error does not affect services. This error is caused by defects of the Oracle JVM, but not the platform code. There is the fault tolerance mechanism for Executors in Spark: the Stage retries in case of an Executor crash to ensure the success execution of tasks.
