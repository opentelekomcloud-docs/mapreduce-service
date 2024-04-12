:original_name: mrs_01_24024.html

.. _mrs_01_24024:

Managing Jobs on the Flink Web UI
=================================

Scenario
--------

Define Flink jobs, including Flink SQL and Flink JAR jobs.

.. _mrs_01_24024__en-us_topic_0000001173470782_section1746418521537:

Creating a Job
--------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.

#. Click **Job Management**. The job management page is displayed.

#. Click **Create Job**. On the displayed job creation page, set parameters by referring to :ref:`Table 1 <mrs_01_24024__en-us_topic_0000001173470782_table25451917135812>` and click **OK**. The job development page is displayed.

   .. _mrs_01_24024__en-us_topic_0000001173470782_table25451917135812:

   .. table:: **Table 1** Parameters for creating a job

      +-------------+----------------------------------------------------------------------------------------------------------------+
      | Parameter   | Description                                                                                                    |
      +=============+================================================================================================================+
      | Type        | Job type, which can be **Flink SQL** or **Flink Jar**.                                                         |
      +-------------+----------------------------------------------------------------------------------------------------------------+
      | Name        | Job name, which can contain a maximum of 64 characters. Only letters, digits, and underscores (_) are allowed. |
      +-------------+----------------------------------------------------------------------------------------------------------------+
      | Task Type   | Type of the job data source, which can be a stream job or a batch job.                                         |
      +-------------+----------------------------------------------------------------------------------------------------------------+
      | Description | Job description, which can contain a maximum of 100 characters.                                                |
      +-------------+----------------------------------------------------------------------------------------------------------------+

#. .. _mrs_01_24024__en-us_topic_0000001173470782_li3175133444316:

   (Optional) If you need to develop a job immediately, configure the job on the job development page.

   -  .. _mrs_01_24024__en-us_topic_0000001173470782_li1375424453411:

      Creating a Flink SQL job

      a. Develop the job on the job development page.

      b. Click **Check Semantic** to check the input content and click **Format SQL** to format SQL statements.

      c. After the job SQL statements are developed, set running parameters by referring to :ref:`Table 2 <mrs_01_24024__en-us_topic_0000001173470782_table4292165617332>` and click **Save**.

         .. _mrs_01_24024__en-us_topic_0000001173470782_table4292165617332:

         .. table:: **Table 2** Running parameters

            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Parameter                         | Description                                                                                                                                                                                                   |
            +===================================+===============================================================================================================================================================================================================+
            | Parallelism                       | Number of concurrent jobs. The value must be a positive integer containing a maximum of 64 characters.                                                                                                        |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Maximum Operator Parallelism      | Maximum parallelism of operators. The value must be a positive integer containing a maximum of 64 characters.                                                                                                 |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | JobManager Memory (MB)            | Memory of JobManager The minimum value is **512** and the value can contain a maximum of 64 characters.                                                                                                       |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Submit Queue                      | Queue to which a job is submitted. If this parameter is not set, the **default** queue is used. The queue name can contain a maximum of 30 characters. Only letters, digits, and underscores (_) are allowed. |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | taskManager                       | taskManager running parameters include:                                                                                                                                                                       |
            |                                   |                                                                                                                                                                                                               |
            |                                   | -  **Slots**: If this parameter is left blank, the default value **1** is used.                                                                                                                               |
            |                                   | -  **Memory (MB)**: The minimum value is **512**.                                                                                                                                                             |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Enable CheckPoint                 | Whether to enable CheckPoint. After CheckPoint is enabled, you need to configure the following information:                                                                                                   |
            |                                   |                                                                                                                                                                                                               |
            |                                   | -  **Time Interval (ms)**: This parameter is mandatory.                                                                                                                                                       |
            |                                   |                                                                                                                                                                                                               |
            |                                   | -  **Mode**: This parameter is mandatory.                                                                                                                                                                     |
            |                                   |                                                                                                                                                                                                               |
            |                                   |    The options are **EXACTLY_ONCE** and **AT_LEAST_ONCE**.                                                                                                                                                    |
            |                                   |                                                                                                                                                                                                               |
            |                                   | -  **Minimum Interval (ms)**: The minimum value is **10**.                                                                                                                                                    |
            |                                   |                                                                                                                                                                                                               |
            |                                   | -  **Timeout Duration**: The minimum value is **10**.                                                                                                                                                         |
            |                                   |                                                                                                                                                                                                               |
            |                                   | -  **Maximum Parallelism**: The value must be a positive integer containing a maximum of 64 characters.                                                                                                       |
            |                                   |                                                                                                                                                                                                               |
            |                                   | -  **Whether to clean up**: This parameter can be set to **Yes** or **No**.                                                                                                                                   |
            |                                   |                                                                                                                                                                                                               |
            |                                   | -  **Whether to enable incremental checkpoints**: This parameter can be set to **Yes** or **No**.                                                                                                             |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Failure Recovery Policy           | Failure recovery policy of a job. The options are as follows:                                                                                                                                                 |
            |                                   |                                                                                                                                                                                                               |
            |                                   | -  **fixed-delay**: You need to configure **Retry Times** and **Retry Interval (s)**.                                                                                                                         |
            |                                   | -  **failure-rate**: You need to configure **Max Retry Times**, **Interval (min)**, and **Retry Interval (s)**.                                                                                               |
            |                                   | -  **none**                                                                                                                                                                                                   |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

      d. Click **Submit** in the upper left corner to submit the job.

   -  Creating a Flink JAR job

      a. Click **Select**, upload a local JAR file, and set parameters by referring to :ref:`Table 3 <mrs_01_24024__en-us_topic_0000001173470782_table1388311381402>`.

         .. _mrs_01_24024__en-us_topic_0000001173470782_table1388311381402:

         .. table:: **Table 3** Parameter configuration

            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Parameter                         | Description                                                                                                                                                                                                   |
            +===================================+===============================================================================================================================================================================================================+
            | Local .jar File                   | Upload a local JAR file. The size of the file cannot exceed 10 MB.                                                                                                                                            |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Main Class                        | Main-Class type.                                                                                                                                                                                              |
            |                                   |                                                                                                                                                                                                               |
            |                                   | -  **Default**: By default, the class name is specified based on the **Mainfest** file in the JAR file.                                                                                                       |
            |                                   | -  **Specify**: Manually specify the class name.                                                                                                                                                              |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Type                              | Class name.                                                                                                                                                                                                   |
            |                                   |                                                                                                                                                                                                               |
            |                                   | This parameter is available when **Main Class** is set to **Specify**.                                                                                                                                        |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Class Parameter                   | Class parameters of Main-Class (parameters are separated by spaces).                                                                                                                                          |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Parallelism                       | Number of concurrent jobs. The value must be a positive integer containing a maximum of 64 characters.                                                                                                        |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | JobManager Memory (MB)            | Memory of JobManager The minimum value is **512** and the value can contain a maximum of 64 characters.                                                                                                       |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | Submit Queue                      | Queue to which a job is submitted. If this parameter is not set, the **default** queue is used. The queue name can contain a maximum of 30 characters. Only letters, digits, and underscores (_) are allowed. |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
            | taskManager                       | taskManager running parameters include:                                                                                                                                                                       |
            |                                   |                                                                                                                                                                                                               |
            |                                   | -  **Slots**: If this parameter is left blank, the default value **1** is used.                                                                                                                               |
            |                                   | -  **Memory (MB)**: The minimum value is **512**.                                                                                                                                                             |
            +-----------------------------------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

      b. Click **Save** to save the configuration and click **Submit** to submit the job.

#. Return to the job management page. You can view information about the created job, including job name, type, status, kind, and description.

Starting a Job
--------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Click **Job Management**. The job management page is displayed.
#. In the **Operation** column of the job to be started, click **Start** to run the job. Jobs in the **Draft**, **Saved**, **Submission failed**, **Running succeeded**, **Running failed**, or **Stop** state can be started.

Developing a Job
----------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Click **Job Management**. The job management page is displayed.
#. In the **Operation** column of the job to be developed, click **Develop** to go to the job development page. Develop a job by referring to :ref:`4 <mrs_01_24024__en-us_topic_0000001173470782_li3175133444316>`. You can view created stream tables and fields in the list on the left.

Editing the Job Name and Description
------------------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Click **Job Management**. The job management page is displayed.
#. In the **Operation** column of the item to be modified, click **Edit**, modify **Description**, and click **OK** to save the modification.

Viewing Job Details
-------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Click **Job Management**. The job management page is displayed.
#. In the **Operation** column of the item to be viewed, choose **More** > **Job Monitoring** to view the job running details.

   .. note::

      You can only view details about jobs in the **Running** state.

Checkpoint Failure Recovery
---------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Click **Job Management**. The job management page is displayed.
#. In the Operation column of the item to be restored, click **More** > **Checkpoint Failure Recovery**. You can perform checkpoint failure recovery for jobs in the **Running failed**, **Running Succeeded**, or **Stop** state.

Filtering/Searching for Jobs
----------------------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Click **Job Management**. The job management page is displayed.
#. In the upper right corner of the page, you can obtain job information by selecting the job name, or enter a keyword to search for a job.

Stopping a Job
--------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Click **Job Management**. The job management page is displayed.
#. In the **Operation** column of the item to be stopped, click **Stop**. Jobs in the **Submitting**, **Submission succeeded**, or **Running** state can be stopped.

Deleting a Job
--------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Click **Job Management**. The job management page is displayed.
#. In the **Operation** column of the item to be deleted, click **Delete**, and click **OK** in the displayed page. Jobs in the **Draft**, **Saved**, **Submission failed**, **Running succeeded**, **Running failed**, or **Stop** state can be deleted.
