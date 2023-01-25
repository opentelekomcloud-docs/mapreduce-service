:original_name: admin_guide_000077.html

.. _admin_guide_000077:

Viewing a Health Check Task
===========================

Scenario
--------

Administrators can view all health check tasks in the health check management center to check whether the cluster is affected after the modification.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Choose **O&M** > **Health Check**.

   By default, all saved health check reports are listed. The parameters for a health check report are as follows:

   .. table:: **Table 1** Parametes for a health check report

      +--------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Parameter    | Description                                                                                                                                                                               |
      +==============+===========================================================================================================================================================================================+
      | Check Object | Object to be checked. You can expand the list to view its details.                                                                                                                        |
      +--------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Status       | Check result status. Value options are **No problems found**, **Problems found**, and **Checking**.                                                                                       |
      +--------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Check Type   | Entity on which the check is to be performed. Value options are **System**, **Cluster**, **Host**, **Service**, and **OMS**. If you select **Cluster**, all items are checked by default. |
      +--------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Start Mode   | Whether the health check is automatically or manually performed                                                                                                                           |
      +--------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Started      | Start time of the check                                                                                                                                                                   |
      +--------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Completed    | End time of the check                                                                                                                                                                     |
      +--------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
      | Operation    | Operations you can perform. Value options are **Export Report** and **View Help**.                                                                                                        |
      +--------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

   .. note::

      -  In the upper right corner of the check list, you can filter health checks by check type or status.
      -  If **Check Type** is **Cluster**, **View Help** is displayed in the **Check Object** drop-down list.
      -  During a health check, the system determines whether check objects are healthy based on their historical monitoring metric data.
