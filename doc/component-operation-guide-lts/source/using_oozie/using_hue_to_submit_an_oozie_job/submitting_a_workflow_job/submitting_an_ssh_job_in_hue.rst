:original_name: mrs_01_1831.html

.. _mrs_01_1831:

Submitting an SSH Job in Hue
============================

Scenario
--------

This section guides you to submit an Oozie job of the SSH type on the Hue web UI.

Procedure
---------

#. Create a workflow. For details, see :ref:`Creating a Workflow <mrs_01_1818>`.

#. For details about how to add the trust relationship, see :ref:`Example of Mutual Trust Operations in Hue <mrs_01_1830>`.

#. On the workflow editing page, select the **Ssh** button |image1| and drag it to the operation area.

#. In the **Ssh** window that is displayed, set **User and Host** and **Ssh command** commands and click **Add**.

#. Click |image2| in the upper right corner of the Oozie editor.

   If you need to modify the job name before saving the job (default value: **My Workflow**), click the name directly for modification, for example, **Ssh-Workflow**.

#. After the configuration is saved, click |image3|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

.. |image1| image:: /_static/images/en-us_image_0000001349059981.jpg
.. |image2| image:: /_static/images/en-us_image_0000001296219764.png
.. |image3| image:: /_static/images/en-us_image_0000001348740165.jpg
