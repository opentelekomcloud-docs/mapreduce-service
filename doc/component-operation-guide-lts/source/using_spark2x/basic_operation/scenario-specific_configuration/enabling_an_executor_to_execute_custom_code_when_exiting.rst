:original_name: mrs_01_24805.html

.. _mrs_01_24805:

Enabling an Executor to Execute Custom Code When Exiting
========================================================

.. note::

   This section applies only to MRS 3.2.0 or later.

Scenario
--------

You can configure the following parameters to execute custom code when Executor exits.

Configuration Parameters
------------------------

Configure the following parameters in the **spark-defaults.conf** file of the Spark client.

+-----------------------------------------------------+----------------------------------------------------------------------------------------------------+---------------+
| Parameter                                           | Description                                                                                        | Default Value |
+=====================================================+====================================================================================================+===============+
| spark.executor.execute.shutdown.cleaner             | If this parameter is set to **true**, an executor can execute custom code when the executor exits. | false         |
+-----------------------------------------------------+----------------------------------------------------------------------------------------------------+---------------+
| spark.executor.execute.shutdown.cleaner.max.timeout | Timeout interval for an executor to execute custom code.                                           | 240s          |
+-----------------------------------------------------+----------------------------------------------------------------------------------------------------+---------------+
