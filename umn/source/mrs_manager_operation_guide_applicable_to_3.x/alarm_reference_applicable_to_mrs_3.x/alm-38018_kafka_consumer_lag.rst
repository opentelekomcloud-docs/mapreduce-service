:original_name: ALM-38018.html

.. _ALM-38018:

ALM-38018 Kafka Consumer Lag
============================

Alarm Description
-----------------

If you have configured a threshold to report Kafka consumer lag on the **Alarms** page of Kafka UI (there is no such rule by default), the system reports the alarm based on the following rules:

The system checks the topics subscribed to by all consumer groups every 60 seconds. This alarm is generated when the system detects that the difference (lag) between the consumption progress (offset) and the log end offset of the latest message generated in the partition is too large for five consecutive times, and the consumer log exceeds the threshold configured in the alarm rule.

This alarm is cleared when the system detects that the difference (lag) between the offsets is lower than the configured threshold for five consecutive times.

.. note::

   This alarm applies only to MRS 3.5.0 or later.

Alarm Attributes
----------------

+-----------------------+---------------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                        | Auto Cleared          |
+=======================+=======================================+=======================+
| 38018                 | Major (manually configured threshold) | Yes                   |
|                       |                                       |                       |
|                       | Major (manually configured threshold) |                       |
+-----------------------+---------------------------------------+-----------------------+

Alarm Parameters
----------------

+------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------+
| Type                   | Parameter     | Description                                                                                                               |
+========================+===============+===========================================================================================================================+
| Location Information   | ServiceName   | Specifies the cluster service for which the alarm was generated.                                                          |
+------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------+
|                        | ConsumerGroup | Name of the Kafka consumer group for which the alarm is generated.                                                        |
+------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------+
| Additional Information | TopicName     | Specifies the Kafka topic for which the alarm is generated.                                                               |
+------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------+
|                        | ConsumerLag   | Specifies the number of messages yet to be consumed by the consumers in the Kafka topic for which the alarm is generated. |
+------------------------+---------------+---------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

Messages in Kafka topics are retained for a limited period (seven days by default). If messages are not consumed in time, data will be lost.

Possible Causes
---------------

-  The new consumer group starts consuming messages from the beginning topic, leading to consumer lag.
-  The threshold of the consumer lag alarm rule configured by the user is too small.
-  The Kafka topic traffic increases sharply, and a large number of messages are generated in a short period of time.
-  It takes a long time for the downstream system to process the Kafka messages in the topic.

Handling Procedure
------------------

**Check whether the consumer group is new.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. View the alarm details. In the **Location** information area, view the name of the Kafka consumer group for which the alarm is generated. In the **Additional Information** area, view the topic name.

#. Check whether the consumer group is new.

   -  If yes, go to :ref:`3 <alm-38018__en-us_topic_0000002032161317_li156961417143415>`.

      .. note::

         In a new consumer group, the new consumer starts consuming messages from the beginning topic, which can cause a consumer lag alarm. This alarm is automatically cleared once the downstream consumer finishes processing the topic messages.

   -  If no, go to :ref:`4 <alm-38018__en-us_topic_0000002032161317_li273518163339>`.

#. .. _alm-38018__en-us_topic_0000002032161317_li156961417143415:

   Wait a moment and then check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-38018__en-us_topic_0000002032161317_li273518163339>`.

**Check whether the alarm rule configuration is improper.**

4. .. _alm-38018__en-us_topic_0000002032161317_li273518163339:

   On MRS Manager, choose **Cluster** > **Services** > **Kafka**. On the right of KafkaManager web UI, click the URL link to access the Kafka UI. Click **Alarms** and check whether the configured threshold of the consumer lag alarm is proper.

   -  If yes, go to :ref:`6 <alm-38018__en-us_topic_0000002032161317_li19942958124019>`.
   -  If no, reconfigure the threshold, save the configuration, and go to :ref:`5 <alm-38018__en-us_topic_0000002032161317_li57351716113312>`.

5. .. _alm-38018__en-us_topic_0000002032161317_li57351716113312:

   Wait 5 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-38018__en-us_topic_0000002032161317_li19942958124019>`.

**Check whether the topic traffic increases sharply.**

6. .. _alm-38018__en-us_topic_0000002032161317_li19942958124019:

   On the Kafka UI, click **Topics** and check whether a large number of messages are generated in a short period of time.

   -  If yes, go to :ref:`7 <alm-38018__en-us_topic_0000002032161317_li16628153918413>`.

      .. note::

         If the alarm is caused by a soaring increase in topic traffic, the alarm is automatically cleared after the downstream system consumes topic messages.

   -  If no, go to :ref:`8 <alm-38018__en-us_topic_0000002032161317_li76201831436>`.

7. .. _alm-38018__en-us_topic_0000002032161317_li16628153918413:

   Wait a moment and then check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-38018__en-us_topic_0000002032161317_li76201831436>`.

**Check whether it takes a long time for the downstream system to process messages in the Kafka topic.**

8. .. _alm-38018__en-us_topic_0000002032161317_li76201831436:

   Check whether the downstream system is consuming messages from the topic at a slow pace.

   -  If yes, go to :ref:`9 <alm-38018__en-us_topic_0000002032161317_li158205287444>`.
   -  If no, go to :ref:`10 <alm-38018__en-us_topic_0000002032161317_li42224042151734>`.

9. .. _alm-38018__en-us_topic_0000002032161317_li158205287444:

   Analyze the reason why downstream jobs cannot quickly consume the topic messages and rectify the fault to accelerate the consumption. Wait 5 minutes and check whether the alarm is automatically cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-38018__en-us_topic_0000002032161317_li42224042151734>`.

**Collect fault information.**

10. .. _alm-38018__en-us_topic_0000002032161317_li42224042151734:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

11. Expand the **Service** drop-down list, and select **Kafka** for the target cluster.

12. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
