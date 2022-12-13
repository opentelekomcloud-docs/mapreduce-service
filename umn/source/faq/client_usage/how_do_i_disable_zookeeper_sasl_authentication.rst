:original_name: mrs_03_1219.html

.. _mrs_03_1219:

How Do I Disable ZooKeeper SASL Authentication?
===============================================

Log in to FusionInsight Manager, choose **Cluster** > **Services** > **ZooKeeper**, click the **Configurations** tab and then **All Configurations**. In the navigation pane on the left, choose **quorumpeer(Role)** > **Customization**, add the **set zookeeper.sasl.disable** parameter, and set its value to **false**. Save the configuration and restart the ZooKeeper service.
