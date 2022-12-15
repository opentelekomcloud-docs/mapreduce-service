:original_name: mrs_08_00121.html

.. _mrs_08_00121:

Hue Basic Principles
====================

Hue is a group of web applications that interact with MRS big data components. It helps you browse HDFS, perform Hive query, and start MapReduce jobs. Hue bears applications that interact with all MRS big data components.

Hue provides the file browser and query editor functions:

-  File browser allows you to directly browse and operate different HDFS directories on the GUI.

-  Query editor can write simple SQL statements to query data stored on Hadoop, for example, HDFS, HBase, and Hive. With the query editor, you can easily create, manage, and execute SQL statements and download the execution results as an Excel file.

On the WebUI provided by Hue, you can perform the following operations on the components:

-  HDFS:

   -  View, create, manage, rename, move, and delete files or directories.
   -  File upload and download
   -  Search for files, directories, file owners, and user groups; change the owners and permissions of the files and directories.
   -  Manually configure HDFS directory storage policies and dynamic storage policies.

-  Hive:

   -  Edit and execute SQL/HQL statements. Save, copy, and edit the SQL/HQL template. Explain SQL/HQL statements. Save the SQL/HQL statement and query it.
   -  Database presentation and data table presentation
   -  Supporting different types of Hadoop storage
   -  Use MetaStore to add, delete, modify, and query databases, tables, and views.

      .. note::

         If Internet Explorer is used to access the Hue page to execute HiveSQL statements, the execution fails, because the browser has functional problems. You are advised to use a compatible browser, for example, Google Chrome.

-  MapReduce: Check MapReduce tasks that are being executed or have been finished in the clusters, including their status, start and end time, and run logs.
-  Oozie: Hue provides the Oozie job manager function, in this case, you can use Oozie in GUI mode.
-  ZooKeeper: Hue provides the ZooKeeper browser function for you to use ZooKeeper in GUI mode.

For details about Hue, visit `https://gethue.com/ <http://gethue.com/>`__.

Architecture
------------

Hue, adopting the MTV (Model-Template-View) design, is a web application program running on Django Python. (Django Python is a web application framework that uses open source codes.)

Hue consists of Supervisor Process and WebServer. Supervisor Process is the core Hue process that manages application processes. Supervisor Process and WebServer interact with applications on WebServer through Thrift/REST APIs, as shown in :ref:`Figure 1 <mrs_08_00121__fig53047075153153>`.

.. _mrs_08_00121__fig53047075153153:

.. figure:: /_static/images/en-us_image_0000001296750298.png
   :alt: **Figure 1** Hue architecture

   **Figure 1** Hue architecture

:ref:`Table 1 <mrs_08_00121__table10504539153153>` describes the components shown in :ref:`Figure 1 <mrs_08_00121__fig53047075153153>`.

.. _mrs_08_00121__table10504539153153:

.. table:: **Table 1** Architecture description

   +-----------------------------------+--------------------------------------------------------------------------------------------------------+
   | Connection Name                   | Description                                                                                            |
   +===================================+========================================================================================================+
   | Supervisor Process                | Manages processes of WebServer applications, such as starting, stopping, and monitoring the processes. |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------+
   | Hue WebServer                     | Provides the following functions through the Django Python web framework:                              |
   |                                   |                                                                                                        |
   |                                   | -  Deploys applications.                                                                               |
   |                                   | -  Provides the GUI.                                                                                   |
   |                                   | -  Connects to databases to store persistent data of applications.                                     |
   +-----------------------------------+--------------------------------------------------------------------------------------------------------+
