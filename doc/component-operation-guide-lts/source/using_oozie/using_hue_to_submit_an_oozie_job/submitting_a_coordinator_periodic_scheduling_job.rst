:original_name: mrs_01_1840.html

.. _mrs_01_1840:

Submitting a Coordinator Periodic Scheduling Job
================================================

Scenario
--------

This section describes how to submit a job of the periodic scheduling type on the Hue web UI.

Prerequisites
-------------

Required workflow jobs have been configured before the coordinator task is submitted.

Procedure
---------

#. Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.
#. In the navigation tree on the left, click |image1| and choose **Schedule** to open the Coordinator editor.
#. On the job editing page, click **My Schedule** to change the job name.
#. Click **Choose a Workflow...** to select the workflow to be orchestrated.
#. Select a workflow, set the job execution frequency as prompted, and click |image2| in the upper right corner to save the workflow job.

   .. note::

      Because the time zone is changed, the difference between the time and the local time may be several hours.

#. Click |image3| in the upper right corner of the editor, set the start value and end value of the time range for executing the scheduled job, and click **Submit** to submit the job.

   .. note::

      Because the time zone is changed, the difference between the time and the local time may be several hours.

.. |image1| image:: /_static/images/en-us_image_0000001296059744.png
.. |image2| image:: /_static/images/en-us_image_0000001296219376.png
.. |image3| image:: /_static/images/en-us_image_0000001348739769.jpg
