:original_name: mrs_01_24796.html

.. _mrs_01_24796:

Error 403 Is Reported When a CDL Job Is Stopped
===============================================

Symptom
-------

The error message "parameter exception with code: 403" is displayed when a CDL job is stopped on the CDLService web UI.

|image1|

Possible Causes
---------------

The current user does not have the permission to stop the job.

Procedure
---------

Stop the job as the user who created the job. To view the job creator, log in to the CDLService web UI, locate the job in the job list, and view the creator in the **Creator** column.

.. |image1| image:: /_static/images/en-us_image_0000001532791956.png
