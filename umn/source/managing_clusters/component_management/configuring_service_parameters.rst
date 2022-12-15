:original_name: mrs_01_0204.html

.. _mrs_01_0204:

Configuring Service Parameters
==============================

On the MRS console, you can view and modify the default service configurations based on site requirements and export or import the configurations.

Impact on the System
--------------------

-  You need to download and update the client configuration files after configuring HBase, HDFS, Hive, Spark, Yarn, and MapReduce service properties.
-  The parameters of DBService cannot be modified when only one DBService role instance exists in the cluster.

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Modifying Service Parameters
----------------------------

#. On the MRS cluster details page, click **Components**.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Configuring Service Parameters <mrs_01_0246>`.

#. Select the target service from the service list.

#. Click **Service Configuration**.

#. Switch **Basic** to **All**. All configuration parameters of the service are displayed in the navigation tree. The service name and role names are displayed from upper to lower in the navigation tree.

#. In the navigation tree, select a specified parameter and change its value. You can also enter the parameter name in the **Search** box to search for the parameter and view the result.

   If you want to cancel the modification of a parameter value, click |image1| to restore it.

#. Click **Save Configuration**, select **Restart the affected services or instances**, and click **OK**.

   .. note::

      To update the queue configuration of Yarn without restarting service, choose **More** > **Refresh Queue** on the **Service Status** tab page to update the queue for the configuration to take effect.

.. |image1| image:: /_static/images/en-us_image_0000001348737945.png
