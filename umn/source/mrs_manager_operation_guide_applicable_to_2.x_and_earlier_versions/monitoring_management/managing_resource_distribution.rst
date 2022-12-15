:original_name: mrs_01_0233.html

.. _mrs_01_0233:

Managing Resource Distribution
==============================

On MRS Manager, you can query the top value curves, bottom value curves, or average data curves of key service and host monitoring metrics, that is, the resource distribution information. MRS Manager allows you to view the monitoring data of the last hour.

You can also modify the resource distribution on MRS Manager to display both the top and bottom value curves in service and host resource distribution figures.

Resource distribution of some monitoring metrics is not recorded.

Procedure
---------

-  View the resource distribution of service monitoring metrics.

   #. On MRS Manager, click **Services**.

   #. Select the target service from the service list.

   #. Click **Resource Distribution**.

      Select key metrics of the service from **Metric**. MRS Manager displays the resource distribution of the metrics in the last hour.

-  View the resource distribution of host monitoring metrics.

   #. Click **Hosts**.

   #. Click the name of the specified host in the host list.

   #. Click **Resource Distribution**.

      Select key metrics of the host from **Metrics**. MRS Manager displays the resource distribution of the metrics in the last hour.

-  Configure resource distribution.

   #. On MRS Manager, click **System**.

   #. In **Configuration**, click **Configure Resource Contribution Ranking** under **Monitoring and Alarm**.

   #. Change the number of resources to be displayed.

      -  Set **Number of Top Resources** to the number of top values.
      -  Set **Number of Bottom Resources** to the number of bottom values.

      .. note::

         The sum of the maximum value and minimum value of resource distribution cannot be greater than 5.

   #. Click **OK** to save the configurations.

      The message "Number of top and bottom resources saved successfully" is displayed in the upper right corner of the page.
