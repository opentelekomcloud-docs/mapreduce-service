:original_name: mrs_01_1733.html

.. _mrs_01_1733:

Importing and Exporting Compute Instance Configurations
=======================================================

Scenarios
---------

On the HetuEngine web UI, you can import or export the instance configuration file and download the instance configuration template.

Prerequisites
-------------

You have created a user for accessing the HetuEngine web UI. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

Procedure
---------

#. Log in to FusionInsight Manager as a user who can access the HetuEngine web UI and choose **Cluster** > **Services** > **HetuEngine**. The **HetuEngine** service page is displayed.
#. In the **Basic Information** area on the **Dashboard** tab page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.

   -  Importing an instance configuration file: Click **Import** above the instance list, select an instance configuration file in JSON format from the local PC, and click **Open**.

      .. important::

         The instance configuration file must be named **upLoadConfig.json** so that it can be imported.

   -  Exporting an instance configuration file: Click **Export** above the instance list to export the current instance configuration file to the local PC.
