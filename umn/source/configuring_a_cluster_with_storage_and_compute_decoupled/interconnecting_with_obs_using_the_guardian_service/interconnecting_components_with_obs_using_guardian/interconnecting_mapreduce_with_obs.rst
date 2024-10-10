:original_name: mrs_01_248998.html

.. _mrs_01_248998:

Interconnecting MapReduce with OBS
==================================

Interconnecting with OBS
------------------------

#. Log in to FusionInsight Manager, choose **Cluster** > **Services** > **MapReduce** and choose **Configurations** > **All Configurations**. In the navigation tree, choose **MapReduce** > **Customization**. In the customized configuration items, add the configuration item **mapreduce.jobhistory.always-scan-user-dir** to **core-site.xml** and set the parameter to **true**.

   |image1|

#. Save the configurations and restart the MapReduce service.

.. |image1| image:: /_static/images/en-us_image_0000001972894066.png
