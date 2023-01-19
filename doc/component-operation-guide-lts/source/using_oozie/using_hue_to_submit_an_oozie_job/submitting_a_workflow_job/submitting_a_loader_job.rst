:original_name: mrs_01_1823.html

.. _mrs_01_1823:

Submitting a Loader Job
=======================

Scenario
--------

This section describes how to submit an Oozie job of the Loader type on the Hue web UI.

Procedure
---------

#. Create a workflow. For details, see :ref:`Creating a Workflow <mrs_01_1818>`.

#. On the workflow editing page, select |image1| next to **Loader** and drag it to the operation area.

#. In the **Loader** window that is displayed, set **Job id**, for example, to **1**. Click **Add**.

   .. note::

      **Job id** is the ID of the Loader job to be orchestrated and can be obtained from the Loader page.

      You can create a Loader job to be scheduled and obtain its job ID. For details, see :ref:`Using Loader <mrs_01_0400>`.

#. Click |image2| in the upper right corner of the Oozie editor.

   If you need to modify the job name before saving the job (default value: **My Workflow**), click the name directly for modification, for example, **Loader-Workflow**.

#. After the configuration is saved, click |image3|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

.. |image1| image:: /_static/images/en-us_image_0000001349259321.jpg
.. |image2| image:: /_static/images/en-us_image_0000001295900184.png
.. |image3| image:: /_static/images/en-us_image_0000001349059873.jpg
