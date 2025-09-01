:original_name: ALM-38012.html

.. _ALM-38012:

ALM-38012 Number of Broker Partitions Exceeds the Threshold
===========================================================

Alarm Description
-----------------

The system checks the number of partitions on each Broker instance of the Kafka service every 30 seconds. You can view the number of partitions on the Broker instance dashboard page. This alarm is generated when the number of partitions on a Broker instance exceeds the threshold. You can choose **O&M** > **Alarm** > **Thresholds** > **Kafka** and change the threshold. This alarm is cleared when the number of partitions is less than or equal to the threshold.

.. note::

   This alarm applies only to MRS 3.5.0 or later.

Alarm Attributes
----------------

+-----------------------+------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                     | Auto Cleared          |
+=======================+====================================+=======================+
| 38012                 | Critical (default threshold: 6000) | Yes                   |
|                       |                                    |                       |
|                       | Major (default threshold: 3000)    |                       |
+-----------------------+------------------------------------+-----------------------+

Alarm Parameters
----------------

+----------------------+-------------+----------------------------------------------------------+
| Type                 | Parameter   | Description                                              |
+======================+=============+==========================================================+
| Location Information | Source      | Specifies the cluster for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated. |
+----------------------+-------------+----------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.    |
+----------------------+-------------+----------------------------------------------------------+

Impact on the System
--------------------

The number of Broker partitions exceeds the threshold. Too many partitions increase the Broker load and cause bottlenecks in memory, disk I/O, and CPU resources. As a result, the request response becomes slow or even times out.

Possible Causes
---------------

-  Broker partitions are unevenly distributed, or the Kafka cluster usage exceeds the specifications.
-  There are many useless topics.

Handling Procedure
------------------

**Check whether partitions are evenly distributed on Broker.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. In the **Location** field of the alarm details, view the service instance and host for which the alarm is generated.

#. Choose **Cluster** > **Services** > **Kafka** > **Chart**, select **Partition** from the **Chart Category** area, zoom in **Number of Partitions-All Instances** in the upper right corner, and click **Distribution** to check whether partitions are evenly distributed on Broker.


   .. figure:: /_static/images/en-us_image_0000002380310204.png
      :alt: **Figure 1** Example of uneven partition distribution on Broker

      **Figure 1** Example of uneven partition distribution on Broker

   -  If yes, go to :ref:`3 <alm-38012__en-us_topic_0000001951604396_li178961341113810>`.
   -  If no, go to :ref:`4 <alm-38012__en-us_topic_0000001951604396_li7896134143815>`.

#. .. _alm-38012__en-us_topic_0000001951604396_li178961341113810:

   If the partitions on Broker are balanced, the Kafka cluster exceeds the specifications. In this case, add Broker instances. Then, go to :ref:`5 <alm-38012__en-us_topic_0000001951604396_li15318844015>`.

   On MRS Manager, choose **Cluster** > **Services** > **Kafka** > **Instances**, click **Add Instance**, and add Broker instances as prompted.

#. .. _alm-38012__en-us_topic_0000001951604396_li7896134143815:

   Click the uneven distribution bar on the rightmost. If the number of partitions on only the Broker node for which the alarm is generated is too large, perform data balancing.

#. .. _alm-38012__en-us_topic_0000001951604396_li15318844015:

   Wait 5 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-38012__en-us_topic_0000001951604396_li884520243019>`.

**Check whether there are many useless topics.**

6. .. _alm-38012__en-us_topic_0000001951604396_li884520243019:

   Check whether useless topics exist in the cluster.

   -  If yes, perform the following steps to delete useless topics: **Deleting topics is a high-risk operation. Before deleting topics, ensure that the topics are not used.**

      a. Log in to Manager as a user who has the permission to access the Kafka web UI.

      b. Choose **Cluster** > **Services** > **Kafka**. On the right of **KafkaManager Web UI**, click the URL to access the Kafka web UI.

      c. Choose **Topics**.

      d. In the **Operation** column of the target topic, click **Action** and select **Delete**.

      e. In the dialog box that is displayed, click **OK**.

         The default built-in topics cannot be deleted.

   -  If no, go to :ref:`8 <alm-38012__en-us_topic_0000001951604396_li1389594103811>`.

7. Wait 5 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-38012__en-us_topic_0000001951604396_li1389594103811>`.

**Collect fault information.**

8.  .. _alm-38012__en-us_topic_0000001951604396_li1389594103811:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **Kafka** for the target cluster.

10. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
