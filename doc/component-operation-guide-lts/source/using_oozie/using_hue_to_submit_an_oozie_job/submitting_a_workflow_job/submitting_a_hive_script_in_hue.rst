:original_name: mrs_01_2372.html

.. _mrs_01_2372:

Submitting a Hive Script in Hue
===============================

Scenario
--------

This section describes how to submit a Hive job on the Hue web UI.

Procedure
---------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

#. In the navigation tree on the left, click |image1| and choose **Workflow** to open the Workflow editor.

#. Click **Documents**, click |image2| to select a Hive script from the operation list, and drag it to the operation page.

#. In the **HiveServer2 Script** dialog box that is displayed, select the saved Hive script. For details about how to save the Hive script, see :ref:`Using HiveQL Editor on the Hue Web UI <mrs_01_0134>`. Select a script and click **Add**.

   |image3|

#. Configure the Job XML, for example, to the HDFS path **/user/admin/examples/apps/hive2/hive-site.xml**. For details, see :ref:`Submitting a Hive2 Job in Hue <mrs_01_1820>`.

#. Click |image4| in the upper right corner of the Oozie editor.

#. After the configuration is saved, click |image5|, and submit the job.

   After the job is submitted, you can view the related contents of the job, such as the detailed information, logs, and processes, on Hue.

.. |image1| image:: /_static/images/en-us_image_0000001349139645.png
.. |image2| image:: /_static/images/en-us_image_0000001295740132.png
.. |image3| image:: /_static/images/en-us_image_0000001296059936.png
.. |image4| image:: /_static/images/en-us_image_0000001295900096.png
.. |image5| image:: /_static/images/en-us_image_0000001349059781.jpg
