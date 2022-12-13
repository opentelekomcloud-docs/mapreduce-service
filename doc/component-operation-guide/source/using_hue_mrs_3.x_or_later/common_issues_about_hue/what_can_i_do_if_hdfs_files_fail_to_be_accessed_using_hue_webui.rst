:original_name: mrs_01_0156.html

.. _mrs_01_0156:

What Can I Do If HDFS Files Fail to Be Accessed Using Hue WebUI?
================================================================

Question
--------

What can I do if an error message shown in the following figure is displayed, indicating that the HDFS file cannot be accessed when I use Hue web UI to access the HDFS file?

|image1|

Answer
------

#. Check whether the user who logs in to the Hue web UI has the permissions of the **hadoop** user group.
#. Check whether the HttpFS instance has been installed for the HDFS service and is running properly. If the HttpFS instance is not installed, manually install and restart the Hue service.

.. |image1| image:: /_static/images/en-us_image_0000001295770320.png
