:original_name: mrs_01_0439.html

.. _mrs_01_0439:

Kafka Cluster Monitoring Management
===================================

This section applies to MRS 1.9.2 clusters.

The Kafka cluster monitoring management includes the following operations:

-  :ref:`Viewing Broker Information <mrs_01_0439__section1254019150558>`
-  :ref:`Viewing Topic Information <mrs_01_0439__section2384151125912>`
-  :ref:`Viewing Consumers Information <mrs_01_0439__section517576022>`
-  :ref:`Modifying the Partition of a Topic Through KafkaManager <mrs_01_0439__section195268241735>`

.. _mrs_01_0439__section1254019150558:

Viewing Broker Information
--------------------------

#. Log in to the KafkaManager web UI.

#. On the cluster list page, click a cluster name to access the Summary page of the cluster.


   .. figure:: /_static/images/en-us_image_0000001349090245.png
      :alt: **Figure 1** Summary page of a cluster

      **Figure 1** Summary page of a cluster

#. Click **Brokers** to access the Broker monitoring page. The page displays the Broker list and I/O statistics of the Broker nodes.


   .. figure:: /_static/images/en-us_image_0000001295770612.png
      :alt: **Figure 2** Broker monitoring page

      **Figure 2** Broker monitoring page

.. _mrs_01_0439__section2384151125912:

Viewing Topic Information
-------------------------

#. Log in to the KafkaManager web UI.

#. On the cluster list page, click a cluster name to access the **Summary** page of the cluster.

#. Choose **Topic** > **List** to view the topic list of the current cluster and information about each topic.


   .. figure:: /_static/images/en-us_image_0000001296250052.png
      :alt: **Figure 3** Topic list

      **Figure 3** Topic list

#. Click a topic name to view details about the topic.


   .. figure:: /_static/images/en-us_image_0000001296090400.png
      :alt: **Figure 4** Topic details

      **Figure 4** Topic details

.. _mrs_01_0439__section517576022:

Viewing Consumers Information
-----------------------------

#. Log in to the KafkaManager web UI.

#. On the cluster list page, click a cluster name to access the **Summary** page of the cluster.

#. Click **Consumers** to view the consumers of the current cluster and each consumer's consumption information.


   .. figure:: /_static/images/en-us_image_0000001295930576.png
      :alt: **Figure 5** Consumers

      **Figure 5** Consumers

#. Click a consumer name to view the list of the consumed topics.


   .. figure:: /_static/images/en-us_image_0000001348770433.png
      :alt: **Figure 6** List of topics consumed by the consumer

      **Figure 6** List of topics consumed by the consumer

#. Click a topic name in the topic list of the consumer to view consumption information about the topic.


   .. figure:: /_static/images/en-us_image_0000001296090404.png
      :alt: **Figure 7** Topic consumption details

      **Figure 7** Topic consumption details

.. _mrs_01_0439__section195268241735:

Modifying the Partition of a Topic Through KafkaManager
-------------------------------------------------------

#. Log in to the KafkaManager web UI.

#. On the cluster list page, click a cluster name to access the **Summary** page of the cluster.

#. Choose **Topic** > **List** to access the topic list page of the current cluster.

#. Click a topic name to access the **Topic Summary** page.

#. Click **Add Partitions**. The page for adding partitions is displayed.


   .. figure:: /_static/images/en-us_image_0000001349090241.png
      :alt: **Figure 8** Adding partitions

      **Figure 8** Adding partitions

#. Confirm the topic name and modify the value of the **Partitions** parameter and click **Add Partitions** to add partitions.


   .. figure:: /_static/images/en-us_image_0000001296250048.png
      :alt: **Figure 9** Modifying the number of partitions

      **Figure 9** Modifying the number of partitions

#. After the partitions are added successfully, click **Go to topic view** to return to the **Topic Summary** page.

#. Check the number of partitions in **Partition Information** in the lower part of the **Topic Summary** page.


   .. figure:: /_static/images/en-us_image_0000001349170145.png
      :alt: **Figure 10** Partition Information

      **Figure 10** Partition Information

#. (Optional) If you are not satisfied with the assigned partitions, you can use the partition reassignment function to automatically reassign partitions.

   a. On the **Topic Summary** page, click **Generate Partition Assignments**.
   b. Select the broker instance and click **Generate Partition Assignments** to generate a partition.
   c. After partition generation, click **Go to topic view** to return to the **Topic Summary** page.
   d. On the **Topic Summary** page, click **Reassign Partitions** to automatically assign partitions to the broker instance of the cluster.
   e. Click **Go to reassign partitions** to view details about the reassigned partitions.

#. (Optional) If you are not satisfied with the automatically assigned partitions, you can manually assign the partitions.

   a. On the **Topic Summary** page, click **Manual Partition Assignments** to access the page for manually assign partitions.
   b. Manually assign a broker ID to each partition replica, and click **Save Partition Assignment** to save the changes.
   c. Click **Go to topic view** to return to the **Topic Summary** page and view the partition details.
