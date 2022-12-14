:original_name: mrs_01_2057.html

.. _mrs_01_2057:

What Can I Do If an Error Occurs when I Access the Application Page Because the Application Cached by HistoryServer Is Recycled?
================================================================================================================================

Question
--------

An error occurs when I access a Spark application page on the HistoryServer page.

Check the HistoryServer logs. The "FileNotFound" exception is found. The related logs are as follows:

.. code-block::

   2016-11-22 23:58:03,694 | WARN  | [qtp55429210-232] | /history/application_1479662594976_0001/stages/stage/ | org.sparkproject.jetty.servlet.ServletHandler.doHandle(ServletHandler.java:628)
   java.io.FileNotFoundException: ${BIGDATA_HOME}/tmp/spark/jobHistoryTemp/blockmgr-5f1f6aca-2303-4290-9845-88fa94d78480/09/temp_shuffle_11f82aaf-e226-46dc-b1f0-002751557694 (No such file or directory)

Answer
------

If a Spark application with a large number of tasks is run on the HistoryServer page, the memory overflows to disk and files with the **temp_shuffle** prefix are generated.

By default, HistoryServer caches 50 Spark applications (determined by the **spark.history.retainedApplications** configuration item). When the number of Spark applications in the memory exceeds 50, HistoryServer reclaims the first cached Spark application and clears the corresponding **temp_shuffle** file.

When a user is viewing Spark applications to be recycled, the **temp_shuffle** file may not be found. As a result, the current page cannot be accessed.

If the preceding problem occurs, use either of the following methods to solve the problem:

-  Access the HistoryServer page of the Spark application again. The correct page information is displayed.

-  If more than 50 Spark applications need to be accessed at the same time, increase the value of **spark.history.retainedApplications**.

   Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Service** > **Spark2x** > **Configuration**, and click **All Configurations**. In the navigation tree on the left, choose **JobHistory2x** > **GUI**, and set parameters.

   .. table:: **Table 1** Parameter description

      +------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
      | Parameter                          | Description                                                                                                                                                                                        | Default Value |
      +====================================+====================================================================================================================================================================================================+===============+
      | spark.history.retainedApplications | Number of Spark applications cached by HistoryServer. When the number of applications to be cached exceeds the value of this parameter, HistoryServer reclaims the first cached Spark application. | 50            |
      +------------------------------------+----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
