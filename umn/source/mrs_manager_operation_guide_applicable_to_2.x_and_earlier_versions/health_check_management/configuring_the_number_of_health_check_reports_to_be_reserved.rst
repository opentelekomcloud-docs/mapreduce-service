:original_name: mrs_01_0277.html

.. _mrs_01_0277:

Configuring the Number of Health Check Reports to Be Reserved
=============================================================

Scenario
--------

Health check reports of MRS clusters, services, and hosts may vary with the time and scenario. You can modify the number of health check reports to be reserved on MRS Manager for later comparison.

This setting is valid for health check reports of clusters, services, and hosts. Report files are saved in **$BIGDATA_DATA_HOME/Manager/healthcheck** on the active management node by default and are automatically synchronized to the standby management node.

Prerequisites
-------------

Users have specified service requirements and planned the save time and health check frequency, and the disk space of the active and standby management nodes is sufficient.

Procedure
---------

#. Choose **System** > **Check Health Status** > **Configure Health Check**.
#. Set **Max. Number of Health Check Reports** to the number of health check reports to be reserved. The value ranges from 1 to 100. The default value is 50.
#. Click **OK** to save the settings. The **Health check configuration saved successfully** is displayed in the upper right corner.
