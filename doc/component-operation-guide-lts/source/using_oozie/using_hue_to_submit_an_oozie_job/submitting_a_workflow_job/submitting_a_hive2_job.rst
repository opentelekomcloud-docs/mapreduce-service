:original_name: mrs_01_1820.html

.. _mrs_01_1820:

Submitting a Hive2 Job
======================

Scenario
--------

This section describes how to submit an Oozie job of the Hive2 type on the Hue web UI.

Procedure
---------

#. Create a workflow. For details, see :ref:`Creating a Workflow <mrs_01_1818>`.

#. On the workflow editing page, select |image1| next to **HiveServer2 Script** and drag it to the operation area.

#. In the **HiveServer2 Script** dialog box that is displayed, configure the script path in the HDFS, for example, **/user/admin/examples/apps/hive2/script.q**, and click **Add**.

#. Click **PARAMETER+** to add input and output parameters.

   For example, if the input parameter is **INPUT=/user/admin/examples/input-data/table**, the output parameter is **OUTPUT=/user/admin/examples/output-data/hive2_workflow**.

   |image2|

#. Click the configuration button |image3| in the upper right corner. On the configuration page that is displayed, click **Delete +** to delete a directory, for example, **/user/admin/examples/output-data/hive2_workflow**.

#. Configure the job XML, for example, to the HDFS path **/user/admin/examples/apps/hive2/hive-site.xml**.

   |image4|

   .. note::

      If the preceding parameters and values are modified, you can query them in **Oozie client installation directory/oozie-client-\*/conf/hive-site.xml**.

#. Click |image5| in the upper right corner of the Oozie editor.

   If you need to modify the job name before saving the job (default value: **My Workflow**), click the name directly for modification, for example, **Hive2-Workflow**.

#. After the configuration is saved, click |image6|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

.. |image1| image:: /_static/images/en-us_image_0000001349259093.jpg
.. |image2| image:: /_static/images/en-us_image_0000001296059796.png
.. |image3| image:: /_static/images/en-us_image_0000001348739821.jpg
.. |image4| image:: /_static/images/en-us_image_0000001348739817.png
.. |image5| image:: /_static/images/en-us_image_0000001295899960.png
.. |image6| image:: /_static/images/en-us_image_0000001349059637.jpg
