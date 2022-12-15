:original_name: mrs_01_1841.html

.. _mrs_01_1841:

Submitting a Bundle Batch Processing Job
========================================

Scenario
--------

In the case that multiple scheduled jobs exist at the same time, you can manage the jobs in batches over the Bundle task. This section describes how to submit a job of the batch type on the Hue web UI.

Prerequisites
-------------

Required related workflow and Coordinator jobs have been configured before the Bundle batch processing job is submitted.

Procedure
---------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

#. In the navigation tree on the left, click |image1| and choose **Bundle** to open the Bundle editor.

#. On the job editing page, click **My Bundle** to change the job name.

#. Click **+Add a coordinator** to select the Coordinator job to be orchestrated.

#. Set the start time and the end time for the scheduled coordinator jobs as prompted and click |image2| in the upper right corner to save the job.

#. Click |image3| in the upper right corner of the editor, select |image4| from the displayed menu, set the start time of the bundle task, click **+Add parameter** to add parameters, and close the dialog box to save the settings.

   |image5|

   .. note::

      Because the time zone is changed, the difference between the time and the local time may be several hours.

#. Click |image6| in the upper right corner of the editor. In the dialog box that is displayed, click **Submit** to submit the job.

.. |image1| image:: /_static/images/en-us_image_0000001296250068.png
.. |image2| image:: /_static/images/en-us_image_0000001295770636.png
.. |image3| image:: /_static/images/en-us_image_0000001295930596.png
.. |image4| image:: /_static/images/en-us_image_0000001296090420.png
.. |image5| image:: /_static/images/en-us_image_0000001296090424.png
.. |image6| image:: /_static/images/en-us_image_0000001295770632.jpg
