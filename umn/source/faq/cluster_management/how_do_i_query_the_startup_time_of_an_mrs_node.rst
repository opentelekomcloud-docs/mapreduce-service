:original_name: mrs_03_1250.html

.. _mrs_03_1250:

How Do I Query the Startup Time of an MRS Node?
===============================================

Log in to the target node and run the following command to query the startup time:

**date -d "$(awk -F. '{print $1}' /proc/uptime) second ago" +"%Y-%m-%d %H:%M:%S"**

|image1|

.. |image1| image:: /_static/images/en-us_image_0000001392574342.png
