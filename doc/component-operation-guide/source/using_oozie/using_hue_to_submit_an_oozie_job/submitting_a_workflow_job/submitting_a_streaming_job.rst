:original_name: mrs_01_1828.html

.. _mrs_01_1828:

Submitting a Streaming Job
==========================

Scenario
--------

This section describes how to submit an Oozie job of the Streaming type on the Hue web UI.

Procedure
---------

#. Create a workflow. For details, see :ref:`Creating a Workflow <mrs_01_1818>`.

#. On the workflow editing page, select |image1| next to **Streaming** and drag it to the operation area.

#. In the **Streaming** window that is displayed, set **Mapper**, for example, to **/bin/cat**. Set **Reducer**, for example, to **/usr/bin/wc**. Click **Add**.

#. Click **FILE+** to add the files required for running.

   for example, **/user/oozie/share/lib/mapreduce-streaming/hadoop-streaming-3.1.1.jar** and **/user/oozie/share/lib/mapreduce-streaming/oozie-sharelib-streaming-5.1.0.jar**.

#. Click the configuration button |image2| in the upper right corner. On the configuration page that is displayed, click **Delete+** to delete a directory, for example, **/user/admin/examples/output-data/streaming_workflow**.

#. Click **PROPERTIES+** to add the following properties:

   -  Enter the property name **mapred.input.dir** in the left box and enter the property value **/user/admin/examples/input-data/text** in the right box.
   -  Enter the property name **mapred.output.dir** in the left box and enter the attribute value **/user/admin/examples/output-data/streaming_workflow** in the right box.

#. Click |image3| in the upper right corner of the Oozie editor.

   If you need to modify the job name before saving the job (default value: **My Workflow**), click the name directly for modification, for example, **Streaming-Workflow**.

#. After the configuration is saved, click |image4|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

.. |image1| image:: /_static/images/en-us_image_0000001348770305.jpg
.. |image2| image:: /_static/images/en-us_image_0000001296249924.jpg
.. |image3| image:: /_static/images/en-us_image_0000001296090268.png
.. |image4| image:: /_static/images/en-us_image_0000001295930444.jpg
