:original_name: mrs_01_24133.html

.. _mrs_01_24133:

Viewing a Consumer Group on Kafka UI
====================================

Scenario
--------

On Kafka UI, you can view the basic information about a consumer group and the consumption status of topics in the group.

Viewing a Consumer Group
------------------------

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.

#. Click **Consumers**. On the consumer group details page that is displayed, you can view all consumer groups in the current cluster and the IP address of the node where each consumer group coordinator is located. In the upper right corner of the page, you can enter a consumer group name to search for the specified consumer group.

   |image1|

#. In the **Consumer Summary** area, you can view the existing consumer groups in the current cluster. You can click a consumer group name to view the topics consumed by the consumer group. Consumed topics can be in the **pending** or **running** state. **pending** indicates that the topic has been consumed but not being consumed. **running** indicates that the topic is being consumed. You can enter a topic name in the upper right corner of the dialog box to filter topics.

   |image2|

#. Click a topic name. On the **Consumer Offsets** page that is displayed, view the topic consumption details.

   |image3|

Viewing the Consumption Lineage Graph
-------------------------------------

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.

#. Click **Consumers**. The consumer group details page is displayed. In the **Active Topic** area, view all consumer groups in the current cluster and topics that are being consumed by each consumer group.

   |image4|

   .. note::

      MRS clusters do not support redirection by clicking a consumer group name.

.. |image1| image:: /_static/images/en-us_image_0000001349139609.png
.. |image2| image:: /_static/images/en-us_image_0000001295900060.png
.. |image3| image:: /_static/images/en-us_image_0000001296059900.png
.. |image4| image:: /_static/images/en-us_image_0000001296219532.png
