:original_name: mrs_01_1826.html

.. _mrs_01_1826:

Submitting a Shell Job
======================

Scenario
--------

This section describes how to submit an Oozie job of the Shell type on the Hue web UI.

Procedure
---------

#. Create a workflow. For details, see :ref:`Creating a Workflow <mrs_01_1818>`.

#. On the workflow editing page, select |image1| next to **Shell** and drag it to the operation area.

#. In the **Shell** window that is displayed, set **Shell command**, for example, to **oozie_shell.sh**, and click **Add**.

#. Click **FILE+** to add the Shell command execution file and Oozie example execution file, for example, **/user/admin/examples/apps/shell/oozie_shell.sh**.

#. Click |image2| in the upper right corner of the Oozie editor.

   If you need to modify the job name before saving the job (default value: **My Workflow**), click the name directly for modification, for example, **Shell-Workflow**.

#. After the configuration is saved, click |image3|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

   .. note::

      -  When configuring a shell command as a Linux command, specify it as the original command instead of the shortcut key command. For example, do not set **ls -l** to **ll**. You can configure it as the shell command **ls**, and add a parameter **-l**.
      -  When uploading the shell script to HDFS on Windows, make sure that the shell script format is Unix. If the format is incorrect, the shell job fails to be submitted.

.. |image1| image:: /_static/images/en-us_image_0000001349059905.jpg
.. |image2| image:: /_static/images/en-us_image_0000001295740256.png
.. |image3| image:: /_static/images/en-us_image_0000001349259357.jpg
