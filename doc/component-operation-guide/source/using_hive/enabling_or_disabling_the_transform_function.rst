:original_name: mrs_01_0958.html

.. _mrs_01_0958:

Enabling or Disabling the Transform Function
============================================

Scenario
--------

The Transform function is not allowed by Hive of the open source version.

MRS Hive supports the configuration of the Transform function. The function is disabled by default, which is the same as that of the open-source community version.

Users can modify configurations of the Transform function to enable the function. However, security risks exist when the Transform function is enabled.

.. note::

   The Transform function can be disabled only in security mode.

Procedure
---------

#. The Hive service configuration page is displayed.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager, choose **Services** > **Hive** > **Service Configuration**, and select **All** from the **Basic** drop-down list.
   -  For MRS 1.9.2 or later, click the cluster name on the MRS console, choose **Components** > **Hive** > **Service Configuration**, and select **All** from the **Basic** drop-down list.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

   -  For MRS 3.\ *x* or later, log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. And choose **Cluster** > *Name of the desired cluster* > **Services** > **Hive** > **Configurations** > **All Configurations**.

#. Enter the parameter name in the search box, search for **hive.security.transform.disallow**, change the parameter value to **true** or **false**, and restart all HiveServer instances.

   .. note::

      -  If this parameter is set to **true**, the Transform function is disabled, which is the same as that in the open-source community version.
      -  If this parameter is set to **false**, the Transform function is enabled, which poses security risks.
