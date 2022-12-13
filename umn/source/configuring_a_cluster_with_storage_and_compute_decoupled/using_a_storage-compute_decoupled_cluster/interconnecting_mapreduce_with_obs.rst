:original_name: mrs_01_0617.html

.. _mrs_01_0617:

Interconnecting MapReduce with OBS
==================================

Before performing the following operations, ensure that you have configured a storage-compute decoupled cluster by referring to :ref:`Configuring a Storage-Compute Decoupled Cluster (Agency) <mrs_01_0768>` or :ref:`Configuring a Storage-Compute Decoupled Cluster (AK/SK) <mrs_01_0468>`.

#. Log in to the MRS management console and click the cluster name to go to the cluster details page.

#. Choose **Components > MapReduce**. The **All Configurations** page is displayed. In the navigation tree on the left, choose **MapReduce > Customization**. In the customized configuration items, add the configuration item **mapreduce.jobhistory.always-scan-user-dir** to **core-site.xml** and set its value to **true**.

   |image1|

#. Save the configurations and restart the MapReduce service.

.. |image1| image:: /_static/images/en-us_image_0000001349257365.png
