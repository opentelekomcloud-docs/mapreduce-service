:original_name: mrs_01_0206.html

.. _mrs_01_0206:

Synchronizing Service Configuration
===================================

Scenario
--------

If **Configuration Status** of some services is **Configuration expired** or **Configuration failed**, synchronize configuration for the cluster or service to restore its configuration status. If all services in the cluster are in the **Configuration failed** state, synchronize the cluster configuration with the background configuration.

Impact on the System
--------------------

After synchronizing service configurations, you need to restart the services whose configurations have expired. These services are unavailable during restart.

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS cluster details page, click **Components**.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Synchronizing Service Configurations <mrs_01_0248>`.

#. Select the target service from the service list.
#. On the Service Status tab page, choose **More** > **Synchronize Configuration**.
#. In the dialog box that is displayed, select **Restart the service or instances whose configurations have expired** and click **Yes** to restart the service.
