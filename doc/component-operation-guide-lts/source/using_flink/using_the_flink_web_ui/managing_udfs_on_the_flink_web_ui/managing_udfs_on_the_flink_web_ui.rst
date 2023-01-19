:original_name: mrs_01_24211.html

.. _mrs_01_24211:

Managing UDFs on the Flink Web UI
=================================

You can customize functions to extend SQL statements to meet personalized requirements. These functions are called user-defined functions (UDFs). You can upload and manage UDF JAR files on the Flink web UI and call UDFs when running jobs.

Flink supports the following three types of UDFs, as described in :ref:`Table 1 <mrs_01_24211__en-us_topic_0000001173470778_table6945142055011>`.

.. _mrs_01_24211__en-us_topic_0000001173470778_table6945142055011:

.. table:: **Table 1** Function classification

   +-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | Type                                      | Description                                                                                                                                    |
   +===========================================+================================================================================================================================================+
   | User-defined Scalar function (UDF)        | Supports one or more input parameters and returns a single result value. For details, see :ref:`UDF Java and SQL Examples <mrs_01_24224>`.     |
   +-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | User-defined aggregation function (UDAF)  | Aggregates multiple records into one value. For details, see :ref:`UDAF Java and SQL Examples <mrs_01_24225>`.                                 |
   +-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+
   | User-defined table-valued function (UDTF) | Supports one or more input parameters and returns multiple rows or columns. For details, see :ref:`UDTF Java and SQL Examples <mrs_01_24227>`. |
   +-------------------------------------------+------------------------------------------------------------------------------------------------------------------------------------------------+

Prerequisites
-------------

You have prepared a UDF JAR file whose size does not exceed 200 MB.

.. _mrs_01_24211__en-us_topic_0000001173470778_section117082071450:

Uploading a UDF
---------------

#. Access the Flink web UI. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.

#. Click **UDF Management**. The **UDF Management** page is displayed.

#. Click **Add UDF**. Select and upload the prepared UDF JAR file for **Local .jar File**.

#. Enter the UDF name and description and click **OK**.

   .. note::

      A maximum of 10 UDF names can be added. **Name** can be customized. **Type** must correspond to the UDF function in the uploaded UDF JAR file.

#. In the UDF list, you can view information about all UDFs in the current application.

#. (Optional) If you need to run or develop a job immediately, configure the job on the **Job Management** page.

   Click **Job Management**. The job management page is displayed.

   -  Starting a UDF job: In the **Operation** column of the UDF job, click **Start**.
   -  Developing a UDF job: In the **Operation** column of the UDF job, click **Develop**. For details about related parameters, see :ref:`Creating a Flink SQL job <mrs_01_24024__en-us_topic_0000001173470782_li1375424453411>`.
   -  Stopping a UDF job: In the **Operation** column of the UDF job, click **Stop**.
   -  Deleting a UDF job: In the **Operation** column of the UDF job, click **Delete**. Only jobs in the **Stop** state can be deleted.
   -  Editing a UDF job: In the **Operation** column of the UDF job, click **Edit**. Only the description of a job can be modified.
   -  Viewing job details: In the **Operation** column of the UDF job, choose **More** > **Job Monitoring**.
   -  Performing checkpoint failure recovery: In the **Operation** column of the UDF job, choose **More** > **Checkpoint failure recovery** to recover the fault. You can perform checkpoint failure recovery for jobs in the **Running failed**, **Running Succeeded**, or **Stop** state.

Editing a UDF
-------------

#. Upload a UDF JAR file. For details, see :ref:`Uploading a UDF <mrs_01_24211__en-us_topic_0000001173470778_section117082071450>`.
#. In the **Operation** column of the UDF job, click **Edit**. The **Edit UDF** page is displayed.
#. Modify the information and click **OK**.

Deleting a UDF
--------------

#. Upload a UDF JAR file. For details, see :ref:`Uploading a UDF <mrs_01_24211__en-us_topic_0000001173470778_section117082071450>`.
#. In the **Operation** column of the UDF job, click **Delete**. The **Delete UDF** page is displayed.
#. Confirm the information about the UDF to be deleted and click **OK**.

   .. note::

      Only the UDFs that are not used can be deleted.
