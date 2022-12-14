:original_name: mrs_01_2034.html

.. _mrs_01_2034:

Why Is a Task Suspended When the ANALYZE TABLE Statement Is Executed and Resources Are Insufficient?
====================================================================================================

Question
--------

When the **analyze table** statement is executed using spark-sql, the task is suspended and the information below is displayed. Why?

.. code-block::

   spark-sql> analyze table hivetable2 compute statistics;
   Query ID = root_20160716174218_90f55869-000a-40b4-a908-533f63866fed
   Total jobs = 1
   Launching Job 1 out of 1
   Number of reduce tasks is set to 0 since there's no reduce operator
   16/07/20 17:40:56 WARN JobResourceUploader: Hadoop command-line option parsing not performed. Implement the Tool interface and execute your application with ToolRunner to remedy this.
   Starting Job = job_1468982600676_0002, Tracking URL = http://10-120-175-107:8088/proxy/application_1468982600676_0002/
   Kill Command = /opt/hadoopclient/HDFS/hadoop/bin/hadoop job  -kill job_1468982600676_0002

Answer
------

When the statement is executed, the SQL statement starts the **analyze table hivetable2 compute statistics** MapReduce tasks. On the ResourceManager Web UI of Yarn, the task is not executed due to insufficient resources. As a result, the task is suspended.


.. figure:: /_static/images/en-us_image_0000001388066504.png
   :alt: **Figure 1** ResourceManager Web UI

   **Figure 1** ResourceManager Web UI

You are advised to add **noscan** when running the **analyze table** statement. The function of this statement is the same as that of the **analyze table hivetable2 compute statistics** statement. The command is as follows:

.. code-block::

   spark-sql> analyze table hivetable2 compute statistics noscan

This command does not start MapReduce tasks and does not occupy Yarn resources. Therefore, the tasks can be executed.
