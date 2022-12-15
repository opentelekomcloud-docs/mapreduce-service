:original_name: mrs_01_0208.html

.. _mrs_01_0208:

Configuring Role Instance Parameters
====================================

Scenario
--------

You can view and modify default role instance configuration on MRS based on site requirements. The configurations can be imported and exported.

Impact on the System
--------------------

You need to download and update the client configuration files after configuring HBase, HDFS, Hive, Spark, Yarn, and MapReduce service properties.

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Modifying Role Instance Parameters
----------------------------------

#. On the MRS cluster details page, click **Components**.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Configuring Role Instance Parameters <mrs_01_0250>`.

#. Select the target service from the service list.

#. Click the **Instances** tab.

#. Click the target role instance from the role instance list.

#. Click the **Instance Configuration** tab.

#. Switch **Basic** to **All** from the drop-down list on the right of the page. All configuration parameters of the role instance are displayed in the navigation tree.

#. In the navigation tree, select a specified parameter and change its value. You can also enter the parameter name in the **Search** box to search for the parameter and view the result.

   If you want to cancel the modification of a parameter value, click |image1| to restore it.

#. Click **Save Configuration**, select **Restart the affected services or instances**, and click **OK**.

.. |image1| image:: /_static/images/en-us_image_0000001348737945.png
