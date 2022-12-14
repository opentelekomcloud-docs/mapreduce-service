:original_name: mrs_01_2125.html

.. _mrs_01_2125:

Modifying Cluster Service Configuration Parameters
==================================================

-  For MRS 1.9.2 or later: You can modify service configuration parameters on the cluster management page of the MRS management console.

   #. Log in to the MRS console. In the left navigation pane, choose **Clusters** > **Active Clusters**, and click a cluster name.

   #. Choose **Components** > *Name of the desired service* > **Service Configuration**.

      The **Basic Configuration** tab page is displayed by default. To modify more parameters, click the **All Configurations** tab. The navigation tree displays all configuration parameters of the service. The level-1 nodes in the navigation tree are service names or role names. The parameter category is displayed after the level-1 node is expanded.

   #. In the navigation tree, select the specified parameter category and change the parameter values on the right.

      If you are not sure about the location of a parameter, you can enter the parameter name in search box in the upper right corner. The system searches for the parameter in real time and displays the result.

   #. Click **Save Configuration**. In the displayed dialog box, click **OK**.

   #. Wait until the message **Operation successful** is displayed. Click **Finish**.

      The configuration is modified.

      Check whether there is any service whose configuration has expired in the cluster. If yes, restart the corresponding service or role instance for the configuration to take effect. You can also select **Restart the affected services or instances** when saving the configuration. .

-  For MRS 3.\ *x* or earlier: You can log in to MRS Manager to modify service configuration parameters.

   #. Log in to MRS Manager.

   #. Click **Services**.

   #. Click the specified service name on the service management page.

   #. Click **Service Configuration**.

      The **Basic Configuration** tab page is displayed by default. To modify more parameters, click the **All Configurations** tab. The navigation tree displays all configuration parameters of the service. The level-1 nodes in the navigation tree are service names or role names. The parameter category is displayed after the level-1 node is expanded.

   #. In the navigation tree, select the specified parameter category and change the parameter values on the right.

      If you are not sure about the location of a parameter, you can enter the parameter name in search box in the upper right corner. The system searches for the parameter in real time and displays the result.

   #. Click **Save**. In the confirmation dialog box, click **OK**.

   #. Wait until the message **Operation successful** is displayed. Click **Finish**.

      The configuration is modified.

      Check whether there is any service whose configuration has expired in the cluster. If yes, restart the corresponding service or role instance for the configuration to take effect. You can also select **Restart the affected services or instances** when saving the configuration.

-  For MRS 3.\ *x* or later: You can log in to FusionInsight Manager to modify service configuration parameters.

   #. You have logged in to FusionInsight Manager.

   #. Choose **Cluster** > **Service**.

   #. Click the specified service name on the service management page.

   #. Click **Configuration**.

      The **Basic Configuration** tab page is displayed by default. To modify more parameters, click the **All Configurations** tab. The navigation tree displays all configuration parameters of the service. The level-1 nodes in the navigation tree are service names or role names. The parameter category is displayed after the level-1 node is expanded.

   #. In the navigation tree, select the specified parameter category and change the parameter values on the right.

      If you are not sure about the location of a parameter, you can enter the parameter name in search box in the upper right corner. The system searches for the parameter in real time and displays the result.

   #. Click **Save**. In the confirmation dialog box, click **OK**.

   #. Wait until the message **Operation successful** is displayed. Click **Finish**.

      The configuration is modified.

      Check whether there is any service whose configuration has expired in the cluster. If yes, restart the corresponding service or role instance for the configuration to take effect.
