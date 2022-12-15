:original_name: admin_guide_000013.html

.. _admin_guide_000013:

Managing Expired Configurations
===============================

Scenario
--------

If a new configuration needs to be delivered to all services in the cluster, or **Configuration Status** of multiple services changes to **Expired** or **Failed** after a configuration is modified, the configuration parameters of these services are not synchronized and do not take effect. In this case, synchronize the configurations and restart related service instances for the cluster so that the new parameters take effect for all services.

If the configuration of the services in the cluster has been synchronized but do not take effect, you need to restart the instances whose configuration has expired.

Impact on the System
--------------------

-  After synchronizing the cluster configuration, you need to restart the services whose configuration has expired. These services are unavailable during restart.
-  The instances whose configuration has expired are unavailable during restart.

Procedure
---------

**Synchronize the configuration.**

#. Log in to FusionInsight Manager.
#. Choose **Cluster** > *Name of the desired cluster* > **Dashboard**.
#. On this page, choose **More** > **Synchronize Configuration**.
#. In the dialog box that is displayed, click **OK**.

**Restart configuration-expired instances.**

#. Choose **More** > **Restart Configuration-Expired Instances**.

#. In the dialog box that is displayed, enter the password of the current login user and click **OK**.

#. In the displayed dialog box, click **OK**.

   You can click **View Instance** to open the list of all expired instances and confirm that the instances have been restarted.
