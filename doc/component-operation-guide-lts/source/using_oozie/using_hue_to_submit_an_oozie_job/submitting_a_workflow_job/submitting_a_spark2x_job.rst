:original_name: mrs_01_1821.html

.. _mrs_01_1821:

Submitting a Spark2x Job
========================

Scenario
--------

This section describes how to submit an Oozie job of the Spark2x type on Hue.

Procedure
---------

#. Create a workflow. For details, see :ref:`Creating a Workflow <mrs_01_1818>`.

#. On the workflow editing page, select |image1| next to **Spark program** and drag it to the operation area.

#. In the Spark window that is displayed, set the value of **Files**, for example, to **hdfs://hacluster/user/admin/examples/apps/spark2x/lib/oozie-examples.jar**. Set the value of **jar/py name**, for example, to **org.apache.oozie.example.SparkFileCopy**, and click **Add**.

#. Set the value of **Main class**, for example, **org.apache.oozie.example.SparkFileCopy**.

#. Click **PARAMETER+** to add related input and output parameters.

   For example, add the following parameters:

   -  **hdfs://hacluster/user/admin/examples/input-data/text/data.txt**
   -  **hdfs://hacluster/user/admin/examples/output-data/spark_workflow**

#. In the **Options list** text box, specify Spark parameters, for example, **--conf spark.yarn.archive=hdfs://hacluster/user/spark2x/jars/8.1.2.2/spark-archive-2x.zip --conf spark.eventLog.enabled=true --conf spark.eventLog.dir=hdfs://hacluster/spark2xJobHistory2x**.

   .. note::

      The version 8.1.2.2 is used as an example. Replace it with the actual version number.

#. Click the configuration button |image2| in the upper right corner. Set the value of **Spark Master**, for example, to **yarn-cluster**. Set the value of **Mode**, for example, **cluster**.

#. On the configuration page that is displayed, click **Delete +** to delete a directory, for example, **hdfs://hacluster/user/admin/examples/output-data/spark_workflow**.

#. Click **PROPERTIES+** and add **sharelib** used by Oozie. Enter the attribute name **oozie.action.sharelib.for.spark** in the left text box and the attribute value **spark2x** in the right text box.

#. Click |image3| in the upper right corner of the Oozie editor.

   If you need to modify the job name before saving the job (default value: **My Workflow**), click the name directly for modification, for example, **Spark-Workflow**.

#. After the configuration is saved, click |image4|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

.. |image1| image:: /_static/images/en-us_image_0000001348739877.jpg
.. |image2| image:: /_static/images/en-us_image_0000001296219484.jpg
.. |image3| image:: /_static/images/en-us_image_0000001349059693.png
.. |image4| image:: /_static/images/en-us_image_0000001295900016.jpg
