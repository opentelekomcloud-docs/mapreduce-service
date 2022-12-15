:original_name: mrs_01_0210.html

.. _mrs_01_0210:

Decommissioning and Recommissioning a Role Instance
===================================================

Scenario
--------

If a Core or Task node is faulty, the cluster status may be displayed as **Abnormal**. In an MRS cluster, data can be stored on different Core nodes. You can decommission the specified role instance on MRS to stop the role instance from providing services. After fault rectification, you can recommission the role instance.

The following role instances can be decommissioned or recommissioned:

-  DataNode role instance on HDFS
-  NodeManager role instance on Yarn
-  RegionServer role instance on HBase
-  ClickHouseServer role instance on ClickHouse
-  Broker role instance on Kafka

Restrictions:

-  If the number of the DataNodes is less than or equal to that of HDFS copies, decommissioning cannot be performed. If the number of HDFS copies is three and the number of DataNodes is less than four in the system, decommissioning cannot be performed. In this case, an error will be reported and force MRS to exit the decommissioning 30 minutes after MRS attempts to perform the decommissioning.
-  If the number of Kafka Broker instances is less than or equal to that of Kafka copies, decommissioning cannot be performed. For example, if the number of Kafka copies is two and the number of nodes is less than three in the system, decommissioning cannot be performed. Instance decommissioning will fail and exit.
-  If a role instance is out of service, you must recommission the instance to start it before using it again.

Prerequisites
-------------

You have synchronized IAM users. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

Procedure
---------

#. On the MRS cluster details page, click **Components**.

   .. note::

      For versions earlier than MRS 1.7.2, see :ref:`Decommissioning and Recommissioning a Role Instance <mrs_01_0252>`.

#. Click a service in the service list.
#. Click the **Instances** tab.
#. Select an instance.
#. Choose **More** > **Decommission** or **Recommission** to perform the corresponding operation.

   .. note::

      During the instance decommissioning, if the service corresponding to the instance is restarted in the cluster using another browser, MRS displays a message indicating that the instance decommissioning is stopped, but the **Operating Status** of the instance is displayed as **Started**. In this case, the instance has been decommissioned on the background. You need to decommission the instance again to synchronize the operating status.
