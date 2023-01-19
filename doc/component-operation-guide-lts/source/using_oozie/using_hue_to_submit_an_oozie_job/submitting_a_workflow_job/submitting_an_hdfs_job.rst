:original_name: mrs_01_1827.html

.. _mrs_01_1827:

Submitting an HDFS Job
======================

Scenario
--------

This section describes how to submit an Oozie job of the HDFS type on the Hue web UI.

Procedure
---------

#. Create a workflow. For details, see :ref:`Creating a Workflow <mrs_01_1818>`.

#. On the workflow editing page, select |image1| next to **Fs** and drag it to the operation area.

#. In the **Fs** window that is displayed, click **Add**.

#. Click **CREATE DIRECTORY+** to add the HDFS directories to be created, for example, **/user/admin/examples/output-data/mkdir_workflow** and **/user/admin/examples/output-data/mkdir_workflow1**.

#. Click |image2| in the upper right corner of the Oozie editor.

   If you need to modify the job name before saving the job (default value: **My Workflow**), click the name directly for modification, for example, **HDFS-Workflow**.

#. After the configuration is saved, click |image3|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

.. |image1| image:: /_static/images/en-us_image_0000001348740093.jpg
.. |image2| image:: /_static/images/en-us_image_0000001296060064.png
.. |image3| image:: /_static/images/en-us_image_0000001295900224.jpg
