:original_name: mrs_01_1963.html

.. _mrs_01_1963:

Configuring Spark2x Web UI ACLs
===============================

Scenario
--------

Users need to implement security protection for Spark2x web UI when some data on the UI cannot be viewed by other users. Once a user attempts to log in to the UI, Spark2x can check the view ACL of the user to determine whether to allow the user to access the UI.

Spark2x has two types of web UI. One is for running tasks. You can access the web UI using the application link on the native Yarn page or the REST APIs. The other one is for ended tasks. You can access the web UI using the Spark2x JobHistory service or the REST APIs. Spark2x and Spark configurations differ from each other.

-  Configuring the ACL of the web UI for running tasks

   Use the following parameters for configuration:

   -  **spark.admin.acls**: specifies the web UI administrator list.
   -  **spark.admin.acls.groups**: specifies the administrator group list.
   -  **spark.ui.view.acls**: specifies the Yarn page visitor list.
   -  **spark.modify.acls.groups**: specifies the Yarn page visitor group list.
   -  **spark.modify.acls**: specifies the web UI modifier list.
   -  **spark.ui.view.acls.groups**: specifies the web UI modifier group list.

-  Configuring the ACL of the web UI for ended tasks

   For ended tasks, use client parameter **spark.history.ui.acls.enable** to enable or disable the ACL access permission.

   If ACL control is enabled, configure client parameters **spark.admin.acls** and **spark.admin.acls.groups** to specify the web UI administrator list and administrator group list. Use client parameters **spark.ui.view.acls** and **spark.modify.acls.groups** to specify the visitor list and visitor group list that view web UI task details. Use client parameters **spark.modify.acls** and **spark.ui.view.acls.groups** to specify the visitor list and group list that modify web UI task details.

Configuration
-------------

Log in to FusionInsight Manager, choose **Cluster > Name of the desired cluster > Services > Spark2x > Configurations**, click **All Configurations**, search for **acl**, and modify the following parameters on the JobHistory, JDBCServer, SparkResource, and Spark pages.

.. table:: **Table 1** Parameter description

   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | Parameter                    | Description                                                                                                                                                                                                                                      | Default Value         |
   +==============================+==================================================================================================================================================================================================================================================+=======================+
   | spark.history.ui.acls.enable | Indicates whether JobHistory supports the permission verification of a single task.                                                                                                                                                              | true                  |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.acls.enable            | Indicates whether to enable Spark permission management.                                                                                                                                                                                         | true                  |
   |                              |                                                                                                                                                                                                                                                  |                       |
   |                              | If this function is enabled, the system checks whether the user has the permission to access and modify task information.                                                                                                                        |                       |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.admin.acls             | Indicates the list of Spark administrators. All members in the list have the rights to manage all Spark tasks. You can configure multiple administrators and separate them from each other using commas (,).                                     | admin                 |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.admin.acls.groups      | Indicates the list of Spark administrator groups. All groups in the list have the permission to manage all Spark tasks. You can configure multiple administrator groups and separate them from each other using commas (,).                      | ``-``                 |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.modify.acls            | Indicates the list of members that have the permission to modify Spark tasks. By default, the user who starts a task has the permission to modify the task. You can configure multiple users and separate them from each other using commas (,). | ``-``                 |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.modify.acls.groups     | Indicates the list of groups that have the permission to modify Spark tasks. You can configure multiple groups and separate them from each other using commas (,).                                                                               | ``-``                 |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.ui.view.acls           | Indicates the list of members that have the permission to access Spark tasks. By default, the user who starts a task has the permission to modify the task. You can configure multiple users and separate them from each other using commas (,). | ``-``                 |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+
   | spark.ui.view.acls.groups    | Indicates the list of groups that have the permission to access Spark tasks. You can configure multiple groups and separate them from each other using commas (,).                                                                               | ``-``                 |
   +------------------------------+--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-----------------------+

.. note::

   If you use a client to submit tasks, you must download the client again after modifying the **spark.admin.acls**, **spark.admin.acls.groups**, **spark.modify.acls**, **spark.modify.acls.groups**, **spark.ui.view.acls**, and **spark.ui.view.acls.groups** parameters.
