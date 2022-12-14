:original_name: mrs_01_0144.html

.. _mrs_01_0144:

Oozie on Hue
============

Hue provides the Oozie job manager function, in this case, you can use Oozie in GUI mode.

.. caution::

   The Hue page is used to view and analyze data such as files and tables. Do not perform high-risk management operations such as deleting objects on the page. If an operation is required, you are advised to perform the operation on each component after confirming that the operation has no impact on services. For example, you can use the HDFS client to perform operations on HDFS files and use the Hive client to perform operations on Hive tables.

How to Use Oozie Job Designer
-----------------------------

Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

In the navigation tree on the left, click |image1| and choose **Workflow**.

The job designer allows users to create MapReduce, Java, Streaming, Fs, SSH, Shell and DistCp jobs.

How to Use Dashboard
--------------------

Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

Click **Jobs** in the upper right corner. The **Job Browser** page is displayed.

View the running status of the Workflow, Coordinator, and Bundles jobs.

|image2|

How to Use Editor
-----------------

Access the Hue web UI. For details, see :ref:`Accessing the Hue Web UI <mrs_01_0132>`.

In the navigation tree on the left, click |image3| and choose **Workflow**.

Workflows, Schedule, and Bundle tasks can be created. Existing applications can be submitted for running, shared, copied, and exported.

-  Each Workflow can contain one or more jobs to form a complete workflow for a specified service.

   When creating a Workflow, you can design jobs in the Hue editor and add the jobs to the Workflow.

-  Each Schedule can define a time trigger to periodically execute a specified Workflow. One time trigger cannot execute multiple Workflows.

-  Each Bundles can define a set to execute multiple Schedules so that different Workflows can be executed in batches.

.. |image1| image:: /_static/images/en-us_image_0000001349289821.png
.. |image2| image:: /_static/images/en-us_image_0000001349170237.png
.. |image3| image:: /_static/images/en-us_image_0000001296250144.png
