:original_name: mrs_01_1957.html

.. _mrs_01_1957:

Setting the Log Level Dynamically
=================================

Scenarios
---------

In some scenarios, to locate problems or check information by changing the log level,

you can add the **-Dlog4j.configuration.watch=true** parameter to the JVM parameter of a process before the process is started. After the process is started, you can modify the log4j configuration file corresponding to the process to change the log level.

The following processes support the dynamic setting of log levels: driver, executor, ApplicationMaster, JobHistory and JDBCServer.

Allowed log levels are as follows: FATAL, ERROR, WARN, INFO, DEBUG, TRACE, and ALL.

Configuration Description
-------------------------

Add the following parameters to the JVM parameter corresponding to a process.

.. table:: **Table 1** Parameter description

   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+
   | Parameter                   | Description                                                                                                                       | Default Value                                                                   |
   +=============================+===================================================================================================================================+=================================================================================+
   | -Dlog4j.configuration.watch | Indicates a JVM parameter of a process. If this parameter is set to **true**, the dynamic configuration of log levels is enabled. | Left blank, indicating that the dynamic configuration of log levels is disabled |
   +-----------------------------+-----------------------------------------------------------------------------------------------------------------------------------+---------------------------------------------------------------------------------+

:ref:`Table 2 <mrs_01_1957__te63dc901a739455981a4564929997088>` lists the JVM parameters of the driver, executor, and ApplicationMaster processes. Configure the following parameters in the **spark-defaults.conf** file on the Spark client. Set the log levels of the driver, executor, and ApplicationMaster processes in the log4j configuration file specified by the **-Dlog4j.configuration** parameter.

.. _mrs_01_1957__te63dc901a739455981a4564929997088:

.. table:: **Table 2** JVM parameters of processes (1)

   +---------------------------------+---------------------------------------------------------------+-------------------+
   | Parameter                       | Description                                                   | Default Log Level |
   +=================================+===============================================================+===================+
   | spark.driver.extraJavaOptions   | Indicates the JVM parameter of the driver process.            | INFO              |
   +---------------------------------+---------------------------------------------------------------+-------------------+
   | spark.executor.extraJavaOptions | Indicates the JVM parameter of the executor process.          | INFO              |
   +---------------------------------+---------------------------------------------------------------+-------------------+
   | spark.yarn.am.extraJavaOptions  | Indicates the JVM parameter of the ApplicationMaster process. | INFO              |
   +---------------------------------+---------------------------------------------------------------+-------------------+

:ref:`Table 3 <mrs_01_1957__t9699ea38453d469a8492f356e2b212cc>` describes the JVM parameters of JobHistory Server and JDBCServer. Set the parameters in the **ENV_VARS** configuration file. Set the log levels of JobHistory Server and JDBCServer in the **log4j.properties** configuration file.

.. _mrs_01_1957__t9699ea38453d469a8492f356e2b212cc:

.. table:: **Table 3** JVM parameters of processes (2)

   +-------------------+---------------------------------------------------------------+-------------------+
   | Parameter         | Description                                                   | Default Log Level |
   +===================+===============================================================+===================+
   | GC_OPTS           | Indicates the JVM parameter of the JobHistory Server process. | INFO              |
   +-------------------+---------------------------------------------------------------+-------------------+
   | SPARK_SUBMIT_OPTS | Indicates the JVM parameter of JDBCServer.                    | INFO              |
   +-------------------+---------------------------------------------------------------+-------------------+

**Example:**

To change the log level of the executor process to DEBUG dynamically, modify the **spark.executor.extraJavaOptions** JVM parameter of the executor process in the **spark-defaults.conf** file and run the following command to add the following configuration before the process is started:

.. code-block::

   -Dlog4j.configuration.watch=true

After the user application is submitted, change the log level in the log4j configuration file (for example, **-Dlog4j.configuration=file:${BIGDATA_HOME}/FusionInsight_Spark2x\_8.1.0.1/install/FusionInsight-Spark2x-3.1.1/spark/conf/log4j-executor.properties**) specified by the **-Dlog4j.configuration** parameter in **spark.executor.extraJavaOptions** to DEBUG:

.. code-block::

   log4j.rootCategory=DEBUG, sparklog

It takes several seconds for the DEBUG level to take effect.
