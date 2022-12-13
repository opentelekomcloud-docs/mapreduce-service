:original_name: mrs_01_0767.html

.. _mrs_01_0767:

Accessing the Spark Web UI
==========================

The Spark web UI is used to view the running status of Spark applications. Google Chrome is recommended for better user experience.

Spark has two web UIs.

-  Spark UI: used to display the status of running applications.

   The UI includes the following parts: Jobs, Stages, Storage, Environment, Executors, SQL, and JDBC/ODBC Server. The Streaming application has the Streaming tab in addition to the preceding parts.

-  History Server UI: used to display the status of Spark applications that are complete or incomplete.

   The UI includes the application ID, application name, start time, end time, execution time, and owner information.

Spark UI
--------

#. Access the component management page.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager and choose **Services**.
   -  For versions earlier than MRS 3.\ *x*, click the cluster name to go to the cluster details page and choose **Components**.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

   -  For MRS 3.\ *x* or later, log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. Choose **Cluster** > *Name of the desired cluster* > **Services**.

#. Select **Yarn**. In the **Yarn Summary** area, click **ResourceManager** in **ResourceManager Web UI** to access the web UI.

#. Locate the Spark application. Click **ApplicationMaster** in the last column of the application information. The Spark UI is displayed.


   .. figure:: /_static/images/en-us_image_0000001388045030.png
      :alt: **Figure 1** ApplicationMaster

      **Figure 1** ApplicationMaster


   .. figure:: /_static/images/en-us_image_0000001295770828.png
      :alt: **Figure 2** Spark UI

      **Figure 2** Spark UI

History Server
--------------

#. Access the component management page.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager and choose **Services**.
   -  For versions earlier than MRS 3.\ *x*, click the cluster name to go to the cluster details page and choose **Components**.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

   -  For MRS 3.\ *x* or later, log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. Choose **Cluster** > *Name of the desired cluster* > **Services**.

#. Select **Spark**. In the **Spark Summary** area, click **JobHistory** corresponding to **Spark Web UI** to access the web UI.


   .. figure:: /_static/images/en-us_image_0000001439698689.png
      :alt: **Figure 3** Spark History Server

      **Figure 3** Spark History Server
