:original_name: admin_guide_000016.html

.. _admin_guide_000016:

Managing Cluster Configurations
===============================

Scenario
--------

MRS Manager allows you to view the changes of service configuration parameters in a cluster with one click, helping you quickly locate faults and improve configuration management efficiency.

You can quickly view all non-default values of each service in the cluster, non-uniform values between instances of the same role, historical records of cluster configuration modifications, and expired parameters in the cluster on the configuration page.

Procedure
---------

#. Log in to MRS Manager.
#. Choose **Cluster** > *Name of the desired cluster* > **Configurations**.
#. Select an operation page based on the scenario.

   -  To view all non-default values:

      a. Click **All Non-default Values**. The system displays the parameters whose values are different from the default values configured for each service, role, or instance in the current cluster.

         You can click |image1| next to a parameter value to quickly restore the value to the default one. You can click |image2| to view the historical modification records of the parameter.

         If there are a large number of parameters to configure, you can filter the parameters in the filter box in the upper right corner of the page or enter keywords in the search box.

      b. To change the values of the parameters, change the values according to the parameter description and click **Save**. In the dialog box that is displayed, click **OK**.

   -  To view all non-uniform values:

      a. Click **All Non-uniform Values**. The system displays parameters with different role, service, instance group, or instance configurations in the current cluster.

         You can click |image3| next to a parameter value and view the differences in the dialog box that is displayed.

      b. To change the value of a parameter, click |image4| to cancel the configuration difference or manually adjust the parameter value, click **OK**, and then click **Save**. In the dialog box that is displayed, click **OK**.

   -  To check expired configurations:

      a. Click **Expired Configurations**. Expired configuration items in the current cluster are displayed.
      b. You can filter services using the service filter box in the upper part of the page to view expired configurations of different services. Alternatively, you can enter keywords in the search box.
      c. Expired configuration items do not take effect completely. Restart the services or instances whose configurations have expired in a timely manner.

   -  To view historical configuration records:

      a. Click **Historical Configurations**. The historical configuration change records of the current cluster are displayed. You can view details about parameter value changes, including the service to which the parameter belongs, parameter values before and after the modification, and parameter files.
      b. To restore a configuration change, click **Restore Configuration** in the **Operation** column of the target record. In the dialog box that is displayed, click **OK**.

   .. note::

      Some configuration items take effect only after the corresponding services are restarted. After the configurations are saved, restart the services or instances whose configurations have expired in a timely manner.

.. |image1| image:: /_static/images/en-us_image_0000001392414378.png
.. |image2| image:: /_static/images/en-us_image_0000001392254854.png
.. |image3| image:: /_static/images/en-us_image_0000001442653641.png
.. |image4| image:: /_static/images/en-us_image_0000001442773609.png
