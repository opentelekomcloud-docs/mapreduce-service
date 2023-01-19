:original_name: mrs_01_2320.html

.. _mrs_01_2320:

Adjusting the Number of Worker Nodes
====================================

Scenarios
---------

On the HetuEngine web UI, you can adjust the number of worker nodes for a compute instance. In this way, resources can be expanded for the compute instance when resources are insufficient and released when the resources are idle. The number of workers can be adjusted manually or automatically.

Prerequisites
-------------

You have created a user for accessing the HetuEngine web UI. For details, see :ref:`Creating a HetuEngine User <mrs_01_1714>`.

.. note::

   -  When an instance is being scaled in or out, the original services are not affected and the instance can still be used.
   -  Instance scale-in/out is delayed to implement smooth adjustment of resource consumption within a long period of time. It cannot respond to the requirements of running SQL tasks for available resources in real time.
   -  After the instance scale-in/out function is enabled, restarting the HSBroker and Yarn services affects the scale-in/out function. If you need to restart the services, you are advised to disable the instance scale-in/out function first.
   -  Before scaling out a compute instance, ensure that the current queue has sufficient resources. Otherwise, the scale-out cannot reach the expected result and subsequent scale-in operations will be affected.
   -  To perform manual scale-in/out, log in to Manager, choose **HetuEngine** > **Configurations** > **All Configurations**, search for **application.customized.properties**, and add the **yarn.hetuserver.engine.flex.timeout.sec** parameter. The default value is **300** (in seconds).

Procedure
---------

#. Log in to FusionInsight Manager as a user who can access the HetuEngine web UI and choose **Cluster** > **Services** > **HetuEngine**. The **HetuEngine** service page is displayed.
#. In the **Basic Information** area on the **Dashboard** tab page, click the link next to **HSConsole WebUI**. The HSConsole page is displayed.
#. Click **Compute Instance**.
#. Locate the row that contains the target instance, and click **Configure** in the **Operation** column.
#. If manual scale-in/out is required, change the number of workers on the configuration page and click **OK**. The compute instance enters the **SCALING OUT** or **SCALING IN** state. After the scale-in/out is complete, the compute instance status changes to **RUNNING**.
#. If automatic scale-in/out is required, choose **Configure Instance** > **Advanced Configuration** and click the **Scaling** switch.

   -  **OFF**: Disable dynamic scale-in/out.

   -  **ON**: Enable dynamic scale-in/out. For details, see :ref:`Table 1 <mrs_01_2320__en-us_topic_0000001219029547_table10789151105917>`. :ref:`Figure 1 <mrs_01_2320__en-us_topic_0000001219029547_fig1841055911467>` shows the configuration page.

      .. _mrs_01_2320__en-us_topic_0000001219029547_table10789151105917:

      .. table:: **Table 1** Parameters for dynamic scale-in/out

         +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
         | Parameter                 | Description                                                                                                                                               | Example Value |
         +===========================+===========================================================================================================================================================+===============+
         | Scale-out Threshold       | When the average value of the instance resource usage in the scale-in/out decision-making period exceeds the threshold, the instance starts to scale out. | 0.9           |
         +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
         | Scale-out Size            | Number of Workers to be added each time when the instance starts to scale out.                                                                            | 1             |
         +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
         | Scale-out Decision Period | Interval for determining whether to scale out an instance. Unit: second                                                                                   | 200           |
         +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
         | Scale-in Threshold        | When the average value of the instance resource usage in the scale-in/out decision-making period exceeds the threshold, the instance starts to scale in.  | 0.1           |
         +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
         | Scale-in Size             | Number of Workers to be reduced each time when the instance starts to scale in.                                                                           | 1             |
         +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
         | Scale-in Decision Period  | Interval for determining whether to scale in an instance. Unit: second                                                                                    | 300           |
         +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
         | Load Collection Period    | Interval for collecting instance load information. Unit: second                                                                                           | 10            |
         +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
         | Scale-out Timeout Period  | Timeout period of the scale-out operation. Unit: second                                                                                                   | 400           |
         +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+
         | Scale-in Timeout Period   | Timeout period of the scale-in operation. Unit: second                                                                                                    | 600           |
         +---------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+

      .. _mrs_01_2320__en-us_topic_0000001219029547_fig1841055911467:

      .. figure:: /_static/images/en-us_image_0000001295899852.png
         :alt: **Figure 1** Scaling out/in an instance

         **Figure 1** Scaling out/in an instance
