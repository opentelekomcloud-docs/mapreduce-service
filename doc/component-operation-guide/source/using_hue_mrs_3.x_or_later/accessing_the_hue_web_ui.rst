:original_name: mrs_01_0132.html

.. _mrs_01_0132:

Accessing the Hue Web UI
========================

Scenario
--------

After Hue is installed in an MRS cluster, users can use Hadoop-related components on the Hue web UI.

This section describes how to open the Hue web UI on the MRS cluster.

.. note::

   To access the Hue web UI, you are advised to use a browser that is compatible with the Hue WebUI, for example, Google Chrome 50. The Internet Explorer may be incompatible with the Hue web UI.

Impact on the System
--------------------

Site trust must be added to the browser when you access Manager and Hue web UI for the first time. Otherwise, the Hue web UI cannot be accessed.

Prerequisites
-------------

When Kerberos authentication is enabled, the MRS cluster administrator has assigned the permission for using Hive to the user. For example, create a human-machine user named **hueuser**, add the user to user groups **hive** (the primary group), **hadoop**, **supergroup**, and **System_administrator**, and assign the **System_administrator** role.

This user is used to log in to Manager.

Procedure
---------

#. Log in to the service page.

   For versions earlier than MRS 3.\ *x*, click the cluster name on the MRS console and choose **Components** > **Hue**.

   For MRS 3.\ *x* or later, log in to FusionInsight Manager (for details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`) and choose **Cluster** > **Services** > **Hue**.

#. On the right of **Hue WebUI**, click the link to open the Hue web UI.

   Hue WebUI provides the following functions:

   -  Click |image1| to execute query statements of Hive and SparkSQL as well as Notebook code. Make sure that Hive and Spark2x have been installed in the MRS cluster before this operation.
   -  Click |image2| to submit workflow tasks, scheduled tasks, and bundle tasks.
   -  Click |image3| to view, import, and export tasks on the Hue web UI, such as workflow tasks, scheduled tasks, and bundle tasks.
   -  Click |image4| to manage metadata in Hive and SparkSQL. Make sure that Hive and Spark2x have been installed in the MRS cluster before this operation.
   -  Click |image5| to view the directories and files in HDFS. Make sure that HDFS has been installed in the MRS cluster before this operation.
   -  Click |image6| to view all jobs in the MRS cluster. Make sure that Yarn has been installed in the MRS cluster before this operation.
   -  Use |image7| to create or query HBase tables. Make sure that the HBase component has been installed in the MRS cluster and the Thrift1Server instance has been added before this operation.
   -  Use |image8| to import data that is in the CSV or TXT format.

   .. note::

      -  When you log in to the Hue web UI as user **hueuser** for the first time, you need to change the password.
      -  After obtaining the URL for accessing the Hue web UI, you can give the URL to other users who cannot access MRS Manager for accessing the Hue web UI.
      -  If you perform operations on the Hue WebUI only but not on Manager, you must enter the password of the current login user when accessing Manager again.

.. |image1| image:: /_static/images/en-us_image_0000001296250156.png
.. |image2| image:: /_static/images/en-us_image_0000001349289833.png
.. |image3| image:: /_static/images/en-us_image_0000001349090353.png
.. |image4| image:: /_static/images/en-us_image_0000001295770724.png
.. |image5| image:: /_static/images/en-us_image_0000001349289837.png
.. |image6| image:: /_static/images/en-us_image_0000001295930684.png
.. |image7| image:: /_static/images/en-us_image_0000001349170249.png
.. |image8| image:: /_static/images/en-us_image_0000001348770541.png
