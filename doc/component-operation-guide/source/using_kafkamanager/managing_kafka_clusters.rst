:original_name: mrs_01_0438.html

.. _mrs_01_0438:

Managing Kafka Clusters
=======================

This section applies to MRS 1.9.2 clusters.

Kafka cluster management includes the following operations:

-  :ref:`Adding a Cluster on the KafkaManager Web UI <mrs_01_0438__section8713185103014>`
-  :ref:`Updating Cluster Parameters <mrs_01_0438__section776745110472>`
-  :ref:`Deleting a Cluster on the KafkaManager Web UI <mrs_01_0438__section656918369521>`

.. _mrs_01_0438__section8713185103014:

Adding a Cluster on the KafkaManager Web UI
-------------------------------------------

After a Kafka cluster is created for the first time, a default Kafka cluster named **my-cluster** is created on the KafkaManager web UI. You can also add Kafka clusters that have been created on the MRS management console on the KafkaManager web UI to manage multiple Kafka clusters.

#. Log in to the KafkaManager web UI.
#. In the upper part of the page, choose **Cluster** > **Add Cluster**.
#. Set the cluster parameters. For the following parameters, refer to their example values. Retain the default values for other parameters.

   .. table:: **Table 1** Cluster parameters to be modified

      +-----------------------------------------------------------------------------+----------------------------------------+-----------------------------------------------------------------------------------------+
      | Parameter                                                                   | Example Value                          | Description                                                                             |
      +=============================================================================+========================================+=========================================================================================+
      | Cluster Name                                                                | mrs-demo                               | Name of the cluster to be added on the KafkaManager web UI                              |
      +-----------------------------------------------------------------------------+----------------------------------------+-----------------------------------------------------------------------------------------+
      | Cluster Zookeeper Hosts                                                     | zk1_ip:zk1_port, zk2_ip:zk2_port/kafka | ZooKeeper address of the cluster to be added                                            |
      +-----------------------------------------------------------------------------+----------------------------------------+-----------------------------------------------------------------------------------------+
      | Kafka Version                                                               | 1.1.0                                  | Kafka version of the cluster to be added. The default value is **1.1.0**.               |
      +-----------------------------------------------------------------------------+----------------------------------------+-----------------------------------------------------------------------------------------+
      | Enable JMX Polling (Set JMX_PORT env variable before starting kafka server) | Selected                               | ``-``                                                                                   |
      +-----------------------------------------------------------------------------+----------------------------------------+-----------------------------------------------------------------------------------------+
      | Poll consumer information (Not recommended for large # of consumers)        | Selected                               | ``-``                                                                                   |
      +-----------------------------------------------------------------------------+----------------------------------------+-----------------------------------------------------------------------------------------+
      | Enable Active OffsetCache (Not recommended for large # of consumers)        | Selected                               | ``-``                                                                                   |
      +-----------------------------------------------------------------------------+----------------------------------------+-----------------------------------------------------------------------------------------+
      | Display Broker and Topic Size (only works after applying this patch)        | Selected                               | ``-``                                                                                   |
      +-----------------------------------------------------------------------------+----------------------------------------+-----------------------------------------------------------------------------------------+
      | Security Protocol                                                           | PLAINTEXT                              | -  For a Kafka cluster with Kerberos authentication enabled, select **SASL_PLAINTEXT**. |
      |                                                                             |                                        | -  For a Kafka cluster with Kerberos authentication disabled, select **PLAINTEXT**.     |
      +-----------------------------------------------------------------------------+----------------------------------------+-----------------------------------------------------------------------------------------+

#. Click **Save**.

.. _mrs_01_0438__section776745110472:

Updating Cluster Parameters
---------------------------

#. Log in to the KafkaManager web UI.
#. Click **Modify** in the **Operations** column of the cluster.
#. Go to the cluster configuration page and modify cluster parameters.

.. _mrs_01_0438__section656918369521:

Deleting a Cluster on the KafkaManager Web UI
---------------------------------------------

#. Log in to the KafkaManager web UI.
#. Click **Disable** in the **Operations** column of the cluster.
#. When **Delete** or **Enable** is displayed in the **Operations** column on the cluster list page, click **Delete** to delete the cluster. You can also click **Enable** to enable the cluster.
