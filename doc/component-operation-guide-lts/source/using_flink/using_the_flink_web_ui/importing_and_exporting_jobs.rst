:original_name: mrs_01_24481.html

.. _mrs_01_24481:

Importing and Exporting Jobs
============================

Scenario
--------

The FlinkServer web UI enables you only to import and export jobs, UDFs, andstream tables.

-  Jobs, flow tables, and UDFs with the same name cannot be imported to the same cluster.
-  When exporting a job, you need to manually select the stream tables and UDFs on which the job depends. Otherwise, a dialog box indicating that the dependent data is not selected will be displayed. The application information of a job will not be exported.
-  When you export a stream table, the application information on which the stream table depends will not be exported.
-  When you export UDFs, the application information on which the UDFs depend and information about jobs used by UDFs will not be exported.
-  Data import and export between different applications. are supported.

Importing a Job
---------------

#. Access the Flink web UI as a user with **FlinkServer Admin Privilege**. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Choose **System Management** > **Import Jobs**.
#. Click **Select** to select a local TAR file and click **OK**. Wait until the file is imported.

   .. note::

      The maximum size of a local TAR file to be uploaded is 200 MB.

Exporting a job
---------------

#. Access the Flink web UI as a user with **FlinkServer Admin Privilege**. For details, see :ref:`Accessing the Flink Web UI <mrs_01_24019>`.
#. Choose **System Management** > **Export Jobs**.
#. Select the data to be exported in either of the following ways. To deselect the content, click **Clear Selected Node**.

   -  Select the data to be exported as required.
   -  Click **Query Regular Expression**. On the displayed page, select the type of the data to be exported (**Table Management**, **Job Management**, or **UDF Management**), enter the keyword, and click **Query**. After the data is successfully matched, click **Synchronize**.

      .. note::

         All matched data will be synchronized after you click **Synchronize**. Currently, you cannot select some data for synchronization.

#. Click **Verify**. After the verification is complete, click **OK**. Wait until the data is exported.
