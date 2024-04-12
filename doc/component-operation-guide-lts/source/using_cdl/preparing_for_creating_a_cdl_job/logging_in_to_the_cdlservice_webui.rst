:original_name: mrs_01_24236.html

.. _mrs_01_24236:

Logging In to the CDLService WebUI
==================================

Scenario
--------

After CDL is installed in an MRS cluster, you can manage data connections and visualized jobs using the CDL web UI.

This section describes how to access the CDL web UI in an MRS cluster.

.. note::

   You are advised to use Google Chrome to access the CDLService web UI because it is incompatible with Internet Explorer.

   CDL cannot fetch tables whose names contain the dollar sign ($) and special characters.

Prerequisites
-------------

-  The CDL component has been installed in an MRS cluster and is running properly.
-  A user with the CDL management permission has been created for the cluster with Kerberos authentication enabled.

Procedure
---------

#. Log in to FusionInsight Manager as a user with the CDL management permissions or the **admin** user (for the cluster where Kerberos authentication is not enabled), and choose **Cluster** > **Services** > **CDL**.

#. On the right of **CDLService UI**, click the link to access the CDLService web UI.

   You can perform the following operations on the CDL web UI:

   -  **Driver Management**: You can upload, view, and delete a driver file corresponding to the connected database.
   -  **Link Management**: You can create, view, edit, and delete a data connection.
   -  **Job Management**: You can create, view, start, pause, restore, stop, restart, delete, or edit a job.
   -  **ENV Management**: You can create, view, edit, and delete Hudi environment variables.
