:original_name: mrs_01_24256.html

.. _mrs_01_24256:

Deleting Residual Information About Flink Tasks
===============================================

Scenario
--------

If a Flink task stops unexpectedly, some directories may reside in the ZooKeeper and HDFS services. To delete the residual directories, set **ClearUpEnabled** to **true**.

Prerequisites
-------------

A FlinkServer instance has been installed in a cluster and is running properly.

Procedure
---------

#. Log in to Manager.

#. Choose **Cluster** > **Services** > **Flink**. On the displayed page, click the **Configurations** tab and then **All Configurations**, search for parameter **ClearUpEnabled**, and set it to **true**. For details about related parameters, see :ref:`Table 1 <mrs_01_24256__en-us_topic_0000001219029127_table133021410550>`.

   .. _mrs_01_24256__en-us_topic_0000001219029127_table133021410550:

   .. table:: **Table 1** Parameters for deleting the residual directories

      +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+------------------+
      | Parameter                     | Description                                                                                                                                                     | Default Value | Value Range      |
      +===============================+=================================================================================================================================================================+===============+==================+
      | ClearUpEnabled                | Specifies whether to delete the residual directories. Set this parameter to **true** if residual directories need to be deleted; set it to **false** otherwise. | true          | true and false   |
      +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+------------------+
      | ClearUpPeriod                 | Specifies the period for deleting residual directories, in minutes.                                                                                             | 1440          | 1440~2147483647  |
      +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+------------------+
      | TrashDirectoryRetentionPeriod | Specifies the period for retaining residual directories, in minutes.                                                                                            | 10080         | 10080~2147483647 |
      +-------------------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------+---------------+------------------+

#. Click **Save**.

   .. important::

      -  This function deletes only the residual directories in the **/flink_base** directory of the ZooKeeper service and the **/flink/recovery** directory of the HDFS service. User-defined directories will not be deleted.
      -  This function does not delete the **checkpoints** directory of the HDFS service. You need to manually delete it.
