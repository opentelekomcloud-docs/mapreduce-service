:original_name: mrs_01_24134.html

.. _mrs_01_24134:

Accessing Kafka UI
==================

Scenario
--------

After the Kafka component is installed in an MRS cluster, you can use Kafka UI to query cluster information, node status, topic partitions, and data production and consumption details. Kafka UI provides a GUI for users to create and delete topics, modify configurations, as well as add and migrate partitions, simplifying user operations and improving O&M efficiency.

Prerequisites
-------------

You have created a user who has the permission to access Kafka UI. To perform related operations on the page, for example, creating a topic, you need to grant related permissions to the user. For details, see :ref:`Managing Kafka User Permissions <mrs_01_0378>`.

Impact on the System
--------------------

Site trust must be added to the browser when you access Manager and Kafka UI for the first time. Otherwise, Kafka UI cannot be accessed.

Procedure
---------

#. Log in to FusionInsight Manager. For details, see\ :ref:`Accessing FusionInsight Manager <mrs_01_2124>`. Choose **Cluster** > **Services** > **Kafka**.

#. On the right of **KafkaManager WebUI**, click the URL to access Kafka UI.

   You can perform the following operations on Kafka UI:

   -  Redistribute partitions in the cluster.
   -  Create, view, and delete topics.
   -  Add partitions to existing topics and modify configurations.
   -  View produced data in a topic.
   -  View broker information.
   -  View the consumption information about the consumer group.
