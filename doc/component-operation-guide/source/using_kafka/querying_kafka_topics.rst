:original_name: mrs_01_0377.html

.. _mrs_01_0377:

Querying Kafka Topics
=====================

Scenario
--------

You can query existing Kafka topics on MRS.

Procedure
---------

#. Go to the Kafka service page.

   -  For versions earlier than MRS 1.9.2, log in to MRS Manager and choose **Services** > **Kafka**.
   -  For MRS 1.9.2 or later, click the cluster name on the MRS console and choose **Components** > **Kafka**.

      .. note::

         If the **Components** tab is unavailable, complete IAM user synchronization first. (On the **Dashboard** page, click **Synchronize** on the right side of **IAM User Sync** to synchronize IAM users.)

   -  For MRS 3.\ *x* or later, log in to FusionInsight Manager. For details, see :ref:`Accessing FusionInsight Manager (MRS 3.x or Later) <mrs_01_2124>`. Choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka**.

#. Click **KafkaTopicMonitor**.

   All topics are displayed in the list by default. You can view the number of partitions and replicas of the topics.

#. Click the desired topic in the list to view its details.
