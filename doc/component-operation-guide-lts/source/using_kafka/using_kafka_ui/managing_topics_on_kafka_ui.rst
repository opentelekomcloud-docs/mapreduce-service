:original_name: mrs_01_24138.html

.. _mrs_01_24138:

Managing Topics on Kafka UI
===========================

Scenario
--------

On Kafka UI, you can view topic details, modify topic configurations, add topic partitions, delete topics, and view the number of data records produced in different time segments in real time.

.. note::

   -  In security mode, Kafka UI does not authenticate the operation of viewing topic details. That is, any user can query topic information. To modify topic configurations, add topic partitions, or delete topics, ensure that the Kafka UI login user belongs to the **kafkaadmin** user group or grant the corresponding operation permissions to the user. Otherwise, the authentication fails.
   -  In non-security mode, Kafka UI does not authenticate any operation.

Viewing Topic Details
---------------------

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.

#. Click **Topics**. The topic management page is displayed.

#. In the **Topic List** area, you can view the names, status, number of partitions, creation time, and number of replicas of topics created in the current cluster.

   |image1|

#. Click a topic name to view details about the topic and partition.

   |image2|

#. In the **Producer Message** area, you can select **Day**, **Week**, or **Month** based on service requirements to view the number of data records produced in the topic.

   |image3|

Modifying the Topic Configuration
---------------------------------

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.
#. Click **Topics**. The topic management page is displayed.

3. In the **Operation** column of the item to be modified, choose **Action** > **Config**. On the displayed page, change the values of **Key** and **Value** of the topic. To add multiple items, click |image4|.
4. Click **OK**.

Searching for a Topic
---------------------

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.
#. Click **Topics**. The topic management page is displayed.
#. In the upper right corner of the page, enter a topic name to search for the topic.

Adding a Partition
------------------

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.
#. Click **Topics**. The topic management page is displayed.
#. In the **Operation** column of the item to be modified, choose **Action** > **Alter**. On the displayed page, modify the topic partition.

   .. note::

      Currently, you can only add partitions to a cluster. That is, the number of partitions after modification must be greater than the number of original partitions.

#. Click **OK**.

Deleting a Topic
----------------

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.
#. Click **Topics**. The topic management page is displayed.
#. In the **Operation** column of the item to be modified, choose **Action** > **Delete**.
#. In the confirmation dialog box that is displayed, click **OK**.

   .. note::

      The default built-in topics cannot be deleted.

Viewing the Number of Data Records Produced
-------------------------------------------

#. Log in to Kafka UI. For details, see :ref:`Accessing Kafka UI <mrs_01_24134>`.

#. Click **Topics**. The topic management page is displayed.

#. In the **Producer Message** area, you can select **Day**, **Week**, or **Month** to view the number of data records produced in different time segments in the current cluster.

   |image5|

.. |image1| image:: /_static/images/en-us_image_0000001296060084.png
.. |image2| image:: /_static/images/en-us_image_0000001349059925.png
.. |image3| image:: /_static/images/en-us_image_0000001296060080.png
.. |image4| image:: /_static/images/en-us_image_0000001348740109.png
.. |image5| image:: /_static/images/en-us_image_0000001349059929.png
