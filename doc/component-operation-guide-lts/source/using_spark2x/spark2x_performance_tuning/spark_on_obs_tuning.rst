:original_name: mrs_01_24056.html

.. _mrs_01_24056:

Spark on OBS Tuning
===================

Scenario
--------

In the scenario where a small number of requests are frequently sent from Spark on OBS to OBS, you can disable OBS monitoring to improve performance.

Configuration
-------------

Modify the configuration in the **core-site.xml** file on the Spark client.

.. table:: **Table 1** Parameter description

   +-------------------------+-------------------------------------------------------------------------------------------------------------------+------------------------------------------------------+
   | Parameter               | Description                                                                                                       | Default Value                                        |
   +=========================+===================================================================================================================+======================================================+
   | fs.obs.metrics.switch   | Specifies whether to report OBS monitoring metrics.                                                               | true                                                 |
   |                         |                                                                                                                   |                                                      |
   |                         | -  **true**: enable                                                                                               |                                                      |
   |                         | -  **false**: disable                                                                                             |                                                      |
   +-------------------------+-------------------------------------------------------------------------------------------------------------------+------------------------------------------------------+
   | fs.obs.metrics.consumer | Specifies the processing mode of OBS monitoring metrics.                                                          | org.apache.hadoop.fs.obs.metrics.OBSAMetricsProvider |
   |                         |                                                                                                                   |                                                      |
   |                         | -  **org.apache.hadoop.fs.obs.metrics.OBSAMetricsProvider**: indicates that OBS monitoring metrics are collected. |                                                      |
   |                         | -  **org.apache.hadoop.fs.obs.DefaultMetricsConsumer**: indicates that OBS monitoring metrics are not collected.  |                                                      |
   |                         |                                                                                                                   |                                                      |
   |                         | To use the OBS monitoring function, ensure that the function of reporting OBS monitoring metrics is enabled.      |                                                      |
   +-------------------------+-------------------------------------------------------------------------------------------------------------------+------------------------------------------------------+
