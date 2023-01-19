:original_name: mrs_01_24135.html

.. _mrs_01_24135:

Kafka UI Overview
=================

Scenario
--------

After logging in to Kafka UI, you can view the basic information about the existing topics, brokers, and consumer groups in the current cluster on the home page. You can also create and delete topics, modify configurations, and add and migrate partitions in the cluster.

Procedure
---------

**Cluster Summary**

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.

#. In the **Cluster Summary** area, view the number of existing topics, brokers, and consumer groups in the current cluster.

   |image1|

#. Click the number under **Brokers**. The **Brokers** page is displayed. For details about the operations on this page, see :ref:`Viewing Brokers on Kafka UI <mrs_01_24139>`.

   Click the number under **Topics**. The **Topics** page is displayed. For details about the operations on this page, see :ref:`Managing Topics on Kafka UI <mrs_01_24138>`.

   Click the number under **Consumer Group**. The **Consumers** page is displayed. For details about the operations on this page, see :ref:`Viewing a Consumer Group on Kafka UI <mrs_01_24133>`.

**Cluster Action**

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.
#. In the **Cluster Action** area, create topics and migrate partitions. For details, see :ref:`Creating a Topic on Kafka UI <mrs_01_24136>` and :ref:`Migrating a Partition on Kafka UI <mrs_01_24137>`.

**Topic Rank**

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.

#. In the **Topic Rank** column, view top 10 topics by the number of topic logs, data volume, incoming data volume, and outgoing data volume in the current cluster.

   |image2|

#. Click a topic name in the **TopicName** column to go to the topic details page. For details about operations on the page, see :ref:`Managing Topics on Kafka UI <mrs_01_24138>`.

.. |image1| image:: /_static/images/en-us_image_0000001295899900.png
.. |image2| image:: /_static/images/en-us_image_0000001349059585.png
