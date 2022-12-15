:original_name: mrs_01_1954.html

.. _mrs_01_1954:

Configuring the Number of Lost Executors Displayed in WebUI
===========================================================

Scenario
--------

In Spark WebUI, the **Executor** page can display information about Lost Executor. Executors are dynamically recycled. If the JDBCServer tasks are large, there may be too many lost executors displayed in WebUI. Therefore, the number of displayed lost executors can be configured.

Procedure
---------

Configure the following parameter in the **spark-defaults.conf** file on Spark client.

.. table:: **Table 1** Parameter description

   +--------------------------------+----------------------------------------------------------------+---------------+
   | Parameter                      | Description                                                    | Default Value |
   +================================+================================================================+===============+
   | spark.ui.retainedDeadExecutors | The maximum number of Lost Executors displayed in Spark WebUI. | 100           |
   +--------------------------------+----------------------------------------------------------------+---------------+
