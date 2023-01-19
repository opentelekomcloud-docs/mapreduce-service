:original_name: mrs_01_1990.html

.. _mrs_01_1990:

Multiple JDBC Clients Concurrently Connecting to JDBCServer
===========================================================

Scenario
--------

Multiple clients can be connected to JDBCServer at the same time. However, if the number of concurrent tasks is too large, the default configuration of JDBCServer must be optimized to adapt to the scenario.

Procedure
---------

#. Set the fair scheduling policy of JDBCServer.

   The default scheduling policy of Spark is **FIFO**, which may cause a failure of short tasks in multi-task scenarios. Therefore, the fair scheduling policy must be used in multi-task scenarios to prevent task failure.

   a. For details about how to configure Fair Scheduler in Spark, visit http://spark.apache.org/docs/3.1.1/job-scheduling.html#scheduling-within-an-application.
   b. Configure Fair Scheduler on the JDBC client.

      #. In the Beeline command line client or the code defined by JDBC, run the following statement:

         **PoolName** is a scheduling pool for Fair Scheduler.

         .. code-block::

            SET spark.sql.thriftserver.scheduler.pool=PoolName;

      #. Run the SQL command. The Spark task will be executed in the preceding scheduling pool.

#. Set the **BroadCastHashJoin** timeout interval.

   There is a timeout parameter of **BroadCastHashJoin**. The task query fails if the query period exceeds the preset timeout interval. In multi-task scenarios, the Spark task of BroadCastHashJoin may fail due to resource preemption. Therefore, it is necessary to modify the timeout interval in the **spark-defaults.conf** file of JDBCServer.

   .. table:: **Table 1** Parameter description

      +----------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------+
      | Parameter                  | Description                                                                                                                                                         | Default Value                                     |
      +============================+=====================================================================================================================================================================+===================================================+
      | spark.sql.broadcastTimeout | The timeout interval in the broadcast table of **BroadcastHashJoin**. If there are many concurrent tasks, set the parameter to a larger value or a negative number. | -1 (Numeral type. The actual value is 5 minutes.) |
      +----------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------+
