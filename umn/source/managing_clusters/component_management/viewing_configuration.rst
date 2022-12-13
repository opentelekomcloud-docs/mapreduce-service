:original_name: mrs_01_0202.html

.. _mrs_01_0202:

Viewing Configuration
=====================

On MRS, you can view the configuration of services (including roles) and role instances.

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

-  Query service configuration.

   #. On the MRS cluster details page, click **Components**.

      .. note::

         For versions earlier than MRS 1.7.2, see :ref:`Viewing Configurations <mrs_01_0244>`.

   #. Select the target service from the service list.

   #. Click **Service Configuration**.

   #. Switch **Basic** to **All**. All configuration parameters of the service are displayed in the navigation tree. The service name and role names are displayed from upper to lower in the navigation tree.

   #. In the navigation tree, select a specified parameter and change its value. You can also enter the parameter name in the **Search** box to search for the parameter and view the result.

      The parameters under the service nodes and role nodes are service configuration parameters and role configuration parameters respectively.

   #. Select **Non-default** from the **--Select--** drop-down list. The parameters whose values are not default values are displayed.

-  Query role instance configurations.

   #. On the MRS cluster details page, click **Components**.

      .. note::

         For versions earlier than MRS 1.7.2, see :ref:`Viewing Configurations <mrs_01_0244>`.

   #. Select the target service from the service list.
   #. Click the **Instances** tab.
   #. Click the target role instance from the role instance list.
   #. Click **Instance Configuration**.
   #. Switch **Basic** to **All** on the right of the page. All configuration parameters of the role instance are displayed in the navigation tree.
   #. In the navigation tree, select a specified parameter and change its value. You can also enter the parameter name in the **Search** box to search for the parameter and view the result.
   #. Select **Non-default** from the **--Select--** drop-down list. The parameters whose values are not default values are displayed.
