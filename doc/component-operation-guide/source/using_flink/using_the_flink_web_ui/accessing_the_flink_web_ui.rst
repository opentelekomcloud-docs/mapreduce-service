:original_name: mrs_01_24019.html

.. _mrs_01_24019:

Accessing the Flink Web UI
==========================

Scenario
--------

After Flink is installed in an MRS cluster, you can connect to clusters and data as well as manage stream tables and jobs using the Flink web UI.

This section describes how to access the Flink web UI in an MRS cluster.

.. note::

   You are advised to use Google Chrome 50 or later to access the Flink web UI. The Internet Explorer may be incompatible with the Flink web UI.

Impact on the System
--------------------

Site trust must be added to the browser when you access Manager and the Flink web UI for the first time. Otherwise, the Flink web UI cannot be accessed.

Procedure
---------

#. Log in to FusionInsight Manager as a user with **FlinkServer Admin Privilege**. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. Choose **Cluster** > **Services** > **Flink**.

#. On the right of **Flink WebUI**, click the link to access the Flink web UI.

   The Flink web UI provides the following functions:

   -  System management:

      -  Cluster connection management allows you to create, view, edit, test, and delete a cluster connection.
      -  Data connection management allows you to create, view, edit, test, and delete a data connection. Data connection types include HDFS and Kafka.
      -  Application management allows you to create, view, and delete an application.

   -  Stream table management allows you to create, view, edit, and delete a stream table.
   -  Job management allows you to create, view, start, develop, edit, stop, and delete a job.
