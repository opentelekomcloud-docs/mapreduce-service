:original_name: mrs_01_24814.html

.. _mrs_01_24814:

Configuring HA for TimelineServer
=================================

Scenario
--------

As a role of the Yarn service, TimelineServer supports the HA mode since the current version. To prevent a single point of failure of TimelineServer, you can enable TimelineServer HA to ensure high availability of the TimelineServer role.

.. note::

   Currently, clusters in IPv6 security mode do not support TimelineServer HA.

   This function applies to MRS 3.2.0-LTS.1 or later.

Impact on the System
--------------------

-  Before the conversion, change the value of **TLS_FLOAT_IP** of TimelineServer to an available floating IP address. (In the case of a single instance, the service IP address of the node is used by default.)
-  During the conversion, the configuration of the TimelineServer role will expire. In this case, you need to restart the instance whose configuration expires.

Procedure
---------

#. Log in to FusionInsight Manager and choose **Cluster** > **Services** > **Yarn**. Click **Configurations**.
#. Change the value of **TLS_FLOAT_IP** to an available floating IP address (the floating IP address and the service IP addresses of the two TimelineServer instances must be in the same network segment) and click **Save** then **OK**.
#. Click the **Instance** tab. Click **Add Instance**, select a node to add a TimelineServer instance, and choose **Next** > **Next** > **Submit**. The instance is added.
#. On FusionInsight Manager, click |image1| next to the cluster name, select **Restart Configuration-Expired Instances**, and wait until the instance is restarted.
#. Check the status of each instance after the restart. For example, the active/standby status and running status of the TimelineServer instances are normal.

.. |image1| image:: /_static/images/en-us_image_0000001533359808.jpg
