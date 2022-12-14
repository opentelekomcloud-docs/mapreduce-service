:original_name: mrs_01_1949.html

.. _mrs_01_1949:

Viewing Aggregated Container Logs on the Web UI
===============================================

Scenarios
---------

When **yarn.log-aggregation-enable** of Yarn is set to **true**, the container log aggregation function is enabled. Log aggregation indicates that after applications are run on Yarn, NodeManager aggregates all container logs of the node to HDFS and deletes local logs. For details, see :ref:`Configuring Container Log Aggregation <mrs_01_0858>`.

However, all logs will be aggregated to an HDFS directory and can only be viewed by accessing an HDFS file. Open-source Spark and Yarn do not support the function of viewing aggregated logs on the web UI.

Spark supports this function. As shown in :ref:`Figure 1 <mrs_01_1949__fig157091128102512>`, the **AggregatedLogs** tab is added to the HistoryServer page. You can click **logs** to view aggregated logs.

.. _mrs_01_1949__fig157091128102512:

.. figure:: /_static/images/en-us_image_0000001387894476.png
   :alt: **Figure 1** Log aggregation page

   **Figure 1** Log aggregation page

Configuration Description
-------------------------

To display logs on the web UI, aggregated logs need to be parsed and presented. Spark parses aggregation logs using JobHistoryServer of Hadoop. Therefore, you can use the **spark.jobhistory.address** parameter to specify the URL of the JobHistoryServer page to parse and present the logs.

**Navigation path for setting parameters:**

When submitting an application, set these parameters using **--conf** or adjust the following parameter in the **spark-defaults.conf** configuration file on the client.

.. note::

   -  This function depends on JobHistoryServer of Hadoop. Therefore, ensure that JobHistoryServer is running properly before using the log aggregation function.
   -  If the parameter value is empty, the **AggregatedLogs** tab page still exists, but you cannot view logs by clicking **logs**.
   -  The aggregated container logs can be viewed only when the application is running and event log files of the application exist on HDFS.
   -  You can click the log link on the **Executors** page to view the logs of a running task. After the task completes, the logs are aggregated to HDFS, and the log link on the **Executors** page becomes invalid. In this case, you can click **logs** on the **AggregatedLogs** page to view the aggregated logs.

.. table:: **Table 1** Parameter description

   +--------------------------+----------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                | Description                                                                                                                            | Default Value         |
   +==========================+========================================================================================================================================+=======================+
   | spark.jobhistory.address | URL of the JobHistoryServer page. The format is *http(s)://ip:port/jobhistory*. For example, **https://10.92.115.1:26014/jobhistory**. | ``-``                 |
   |                          |                                                                                                                                        |                       |
   |                          | The default value is empty, indicating that container aggregation logs cannot be viewed on the web UI.                                 |                       |
   |                          |                                                                                                                                        |                       |
   |                          | Restart the service for the configuration to take effect.                                                                              |                       |
   +--------------------------+----------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
