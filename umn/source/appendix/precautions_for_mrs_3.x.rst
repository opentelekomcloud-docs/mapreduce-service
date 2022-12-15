:original_name: mrs_01_0614.html

.. _mrs_01_0614:

Precautions for MRS 3.x
=======================

Purpose
-------

Custers of versions earlier than MRS 3.x use MRS Manager to manage and monitor MRS clusters. On the Cluster Management page of the MRS management console, you can view cluster details, manage nodes, components, alarms, patches, files, jobs, tenants, and backup and restoration. In addition, you can configure Bootstrap actions and manage tags.

MRS 3.x uses FusionInsight Manager to manage and monitor clusters. On the Cluster Management page of the MRS management console, you can view cluster details, manage nodes, components, alarms, files, jobs, Bootstrap actions, and tags.

Some maintenance operations of the MRS 3.x cluster are different from those of earlier versions. For details, see :ref:`MRS Manager Operation Guide (Applicable to 2.x and Earlier Versions) <mrs_01_0648>` and :ref:`FusionInsight Manager Operation Guide (Applicable to 3.x) <mrs_01_0606>`.

Accessing MRS Manager
---------------------

-  For details about how to access MRS Manager of versions earlier than MRS 3.x, see :ref:`Accessing MRS Manager MRS 2.1.0 or Earlier) <mrs_01_0102>`.
-  For details about how to access FusionInsight Manager of MRS 3.x, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_0129>`.

Modifying MRS Cluster Service Configuration Parameters
------------------------------------------------------

-  For versions earlier than MRS 3.x, you can modify service configuration parameters on the cluster management page of the MRS management console.

   #. Log in to the MRS console. In the left navigation pane, choose **Clusters** > **Active Clusters**, and click a cluster name.

   #. Choose **Components** > *Name of the desired service* > **Service Configuration**.

      The **Basic Configurations** tab page is displayed by default. To modify more parameters, click the **All Configurations** tab. The navigation tree displays all configuration parameters of the service. The level-1 nodes in the navigation tree are service names or role names. The parameter category is displayed after the level-1 node is expanded.

   #. In the navigation tree, select the specified parameter category and change the parameter values on the right.

      If you are not sure about the location of a parameter, you can enter the parameter name in search box in the upper right corner. The system searches for the parameter in real time and displays the result.

   #. Click **Save Configuration**. In the displayed dialog box, click **OK**.

   #. Wait until the message "Operation succeeded" is displayed. Click **Finish**. The configuration is modified.

      Check whether there is any service whose configuration has expired in the cluster. If yes, restart the corresponding service or role instance for the configuration to take effect. You can also select **Restart the affected services or instances** when saving the configuration.

-  In MRS 3.x, you need to log in to FusionInsight Manager to modify service configuration parameters.

   #. Log in to FusionInsight Manager.

   #. Choose **Cluster** > **Services**.

   #. Click the specified service name on the service management page.

   #. Click **Configurations**.

      The **Basic Configurations** tab page is displayed by default. To modify more parameters, click the **All Configurations** tab. The navigation tree displays all configuration parameters of the service. The level-1 nodes in the navigation tree are service names or role names. The parameter category is displayed after the level-1 node is expanded.

   #. In the navigation tree, select the specified parameter category and change the parameter values on the right.

      If you are not sure about the location of a parameter, you can enter the parameter name in search box in the upper right corner. The Manager searches for the parameter in real time and displays the result.

   #. Click **Save**. In the confirmation dialog box, click **OK**.

   #. Wait until the message "Operation succeeded" is displayed. Click **Finish**. The configuration is modified.

      Check whether there is any service whose configuration has expired in the cluster. If yes, restart the corresponding service or role instance for the configuration to take effect.
