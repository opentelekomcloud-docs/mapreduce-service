:original_name: mrs_01_24260.html

.. _mrs_01_24260:

Using Resource Labels to Specify on Which Node Coordinators Should Run
======================================================================

By default, coordinator and worker nodes randomly start on Yarn NodeManager nodes, and you have to open all ports on all NodeManager nodes. Using resource labels of Yarn, HetuEngine allows you to specify NodeManager nodes to run coordinators.

Prerequisites
-------------

You have created a user for accessing the HetuEngine web UI. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

Procedure
---------

#. Log in to FusionInsight Manager as a user who can access the HetuEngine web UI.

#. Set Yarn parameters to specify the scheduler to handle PlacementConstraints.

   a. Choose **Cluster** > **Services** > **Yarn**. Click the **Configurations** tab and then **All Configurations**. On the displayed page, search for **yarn.resourcemanager.placement-constraints.handler**, set **Value** to **scheduler**, and click **Save**.
   b. Click the **Instance** tab, select the active and standby ResourceManager instances, click **More**, and select **Restart Instance** to restart the ResourceManager instances of Yarn. Then wait until they are restarted successfully.

#. .. _mrs_01_24260__en-us_topic_0000001173630826_li163657291812:

   Configure resource labels.

   a. Choose **Tenant Resources** > **Resource Pool**. On the displayed page, click **Add Resource Pool**.
   b. Select a cluster, and enter a resource pool name and a resource label name, for example, **pool1**. Select the desired hosts, click |image1| to add the selected hosts to the new resource pool, and click **OK**.

#. Set HetuEngine parameters to enable the coordinator placement policy and enter the node resource label.

   a. Choose **Cluster** > **Service** > HetuEngine. Click the **Configurations** tab and then **All Configurations**. On the displayed page, set parameters and click **Save**.

      .. table:: **Table 1** Setting HetuEngine parameters

         +------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
         | Parameter                                            | Setting                                                                                                                     |
         +======================================================+=============================================================================================================================+
         | yarn.hetuserver.engine.coordinator.placement.enabled | true                                                                                                                        |
         +------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+
         | yarn.hetuserver.engine.coordinator.placement.label   | Node resource label created in :ref:`3 <mrs_01_24260__en-us_topic_0000001173630826_li163657291812>`, for example, **pool1** |
         +------------------------------------------------------+-----------------------------------------------------------------------------------------------------------------------------+

   b. Click **Dashboard**, click **More**, and select **Service Rolling Restart**. Wait until the HetuEngine service is restarted successfully.

#. Restart the HetuEngine compute instance.

   a. In the **Basic Information** area on the **Dashboard** page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.
   b. Locate the row that contains the target instance and click **Start** in the **Operation** column.

#. Check the node on which the coordinator is running.

   a. Return to FusionInsight Manager.

   b. Choose **Cluster** > **Services** > **Yarn**. In the **Basic Information** area on the **Dashboard** page, click the link next to **ResourceManager WebUI**.

   c. In the navigation pane on the left, choose **Cluster** > **Nodes**. You can view that the coordinator has been started on the node in the resource pool created in :ref:`3 <mrs_01_24260__en-us_topic_0000001173630826_li163657291812>`.

      |image2|

.. |image1| image:: /_static/images/en-us_image_0000001295899908.png
.. |image2| image:: /_static/images/en-us_image_0000001349139461.png
