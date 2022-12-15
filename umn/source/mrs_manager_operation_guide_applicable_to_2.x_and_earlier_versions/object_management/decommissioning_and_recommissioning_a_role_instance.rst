:original_name: mrs_01_0252.html

.. _mrs_01_0252:

Decommissioning and Recommissioning a Role Instance
===================================================

Scenario
--------

If a Core or Task node is faulty, the cluster status may be displayed as **Abnormal**. In an MRS cluster, data can be stored on different Core nodes. Users can decommission the specified role instance on MRS Manager to stop the role instance from providing services. After fault rectification, you can recommission the role instance.

For versions earlier than MRS 1.6.0, the following role instances can be decommissioned and recommissioned.

-  DataNode role instance on HDFS
-  NodeManager role instance on Yarn

The following role instances can be decommissioned and recommissioned for MRS 1.6.0 or later.

-  DataNode role instance on HDFS
-  NodeManager role instance on Yarn
-  RegionServer role instance on HBase
-  Broker role instance on Kafka

Restrictions:

-  If the number of the DataNodes is less than or equal to that of HDFS copies, decommissioning cannot be performed. If the number of HDFS copies is three and the number of DataNodes is less than four in the system, decommissioning cannot be performed. In this case, an error will be reported and the decommissioning will be stopped 30 minutes after the decommissioning attempt is performed on Manager.
-  If the number of Kafka Broker instances is less than or equal to that of copies, decommissioning cannot be performed. For example, if the number of Kafka copies is two and the number of nodes is less than three in the system, decommissioning cannot be performed. Instance decommissioning will fail on Manager and exit.
-  If a role instance is out of service, you must recommission the instance to start it before using it again.

Procedure
---------

#. On MRS Manager page, click **Services**.
#. Click a service in the service list.
#. Click the **Instances** tab.
#. Select an instance.
#. Choose **More** > **Decommission** or **Recommission** to perform the corresponding operation.

   .. note::

      During the instance decommissioning, if the service corresponding to the instance is restarted in the cluster using another browser, MRS Manager displays a message indicating that the instance decommissioning is stopped, but the **Operating Status** of the instance is displayed as **Started**. In this case, the instance has been decommissioned on the background. You need to decommission the instance again to synchronize the operating status.
