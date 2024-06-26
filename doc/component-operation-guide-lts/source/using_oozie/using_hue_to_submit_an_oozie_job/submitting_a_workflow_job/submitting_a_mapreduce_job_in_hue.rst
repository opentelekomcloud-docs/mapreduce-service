:original_name: mrs_01_1824.html

.. _mrs_01_1824:

Submitting a MapReduce Job in Hue
=================================

Scenario
--------

This section describes how to submit an Oozie job of the MapReduce type on the Hue web UI.

Procedure
---------

#. Create a workflow. For details, see :ref:`Creating a Workflow <mrs_01_1818>`.

#. On the workflow editing page, select |image1| next to **MapReduce job** and drag it to the operation area.

#. In the displayed **MapReduce job** dialog box, set **Jar name**, for example, to **/user/admin/examples/apps/map-reduce/lib/oozie-examples-5.1.0.jar**. Click **Add**.

#. Click **PROPERTIES+** to add input and output properties.

   For example, set the value of **mapred.input.dir** to **/user/admin/examples/input-data/text** and set the value of **mapred.output.dir** to **/user/admin/examples/output-data/map-reduce_workflow**.

#. Click the configuration button |image2| in the upper right corner. On the configuration page that is displayed, click **Delete +** to delete a directory, for example, **/user/admin/examples/output-data/map-reduce_workflow**.

#. Click |image3| in the upper right corner of the Oozie editor.

   If you need to modify the job name before saving the job (default value: **My Workflow**), click the name directly for modification, for example, **MapReduce-Workflow**.

#. After the configuration is saved, click |image4|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

.. |image1| image:: /_static/images/en-us_image_0000001349059541.jpg
.. |image2| image:: /_static/images/en-us_image_0000001349258997.jpg
.. |image3| image:: /_static/images/en-us_image_0000001296219324.png
.. |image4| image:: /_static/images/en-us_image_0000001348739717.jpg
