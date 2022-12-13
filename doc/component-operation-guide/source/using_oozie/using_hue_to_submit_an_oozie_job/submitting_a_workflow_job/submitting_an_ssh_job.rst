:original_name: mrs_01_1831.html

.. _mrs_01_1831:

Submitting an SSH Job
=====================

Scenario
--------

This section guides you to submit an Oozie job of the SSH type on the Hue web UI.

Due to security risks, SSH jobs cannot be submitted by default. To use the SSH function, you need to manually enable it.

Procedure
---------

#. Enable the SSH function.

   a. On FusionInsight Manager, choose **Cluster** > **Services** > **Oozie** and click the **Configurations** tab and then **All Configurations**. In the navigation pane on the left, choose **oozie(Role)** > **Security**, change the value of **oozie.job.ssh.enable** to **true**, and click **Save**. In the displayed dialog box, click **OK** to save the configuration.
   b. On the **Dashboard** page of Oozie, choose **More** > **Restart Service** in the upper-right corner to restart Oozie.

#. Create a workflow. For details, see :ref:`Creating a Workflow <mrs_01_1818>`.

#. For details about how to add the trust relationship, see :ref:`Example of Mutual Trust Operations <mrs_01_1830>`.

#. On the workflow editing page, select the **Ssh** button |image1| and drag it to the operation area.

#. In the **Ssh** window that is displayed, set **User and Host** and **Ssh command** commands and click **Add**.

#. Click |image2| in the upper right corner of the Oozie editor.

   If you need to modify the job name before saving the job (default value: **My Workflow**), click the name directly for modification, for example, **Ssh-Workflow**.

#. After the configuration is saved, click |image3|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

.. |image1| image:: /_static/images/en-us_image_0000001296090276.jpg
.. |image2| image:: /_static/images/en-us_image_0000001349289609.png
.. |image3| image:: /_static/images/en-us_image_0000001296249932.jpg
