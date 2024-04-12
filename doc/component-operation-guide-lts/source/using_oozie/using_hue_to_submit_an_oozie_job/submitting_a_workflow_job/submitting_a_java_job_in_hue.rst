:original_name: mrs_01_1822.html

.. _mrs_01_1822:

Submitting a Java Job in Hue
============================

Scenario
--------

This section describes how to submit an Oozie job of the Java type on the Hue web UI.

Procedure
---------

#. Create a workflow. For details, see :ref:`Creating a Workflow <mrs_01_1818>`.

#. On the workflow editing page, select |image1| next to **Java program** and drag it to the operation area.

#. In the **Jar program** window that is displayed, set the value of **Jar name**, for example, **/user/admin/examples/apps/java-main/lib/oozie-examples-5.1.0.jar**. Set the value of **Main class**, for example, **org.apache.oozie.example.DemoJavaMain**. Click **Add**.

#. Click |image2| in the upper right corner of the Oozie editor.

   If you need to modify the job name before saving the job (default value: **My Workflow**), click the name directly for modification, for example, **Java-Workflow**.

#. After the configuration is saved, click |image3|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

.. |image1| image:: /_static/images/en-us_image_0000001296059764.jpg
.. |image2| image:: /_static/images/en-us_image_0000001295739960.png
.. |image3| image:: /_static/images/en-us_image_0000001349059605.jpg
