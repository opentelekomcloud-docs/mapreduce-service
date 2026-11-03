:original_name: ALM-38020.html

.. _ALM-38020:

ALM-38020 Abnormal Kafka Production Traffic
===========================================

Alarm Description
-----------------

If you have configured the rule for reporting the alarm indicating abnormal production traffic using a script (no rule by default), the system checks all configured topics every minute (configurable). This alarm is generated when the production traffic of the configured topics is not within the threshold (unit: number of produced messages per second) for five (configurable) consecutive times.

This alarm is cleared when the production traffic of the configured topics is within the threshold for five consecutive times (configurable). If you perform operations that will stop services, you are advised to mask this alarm.

This section applies to MRS 3.6.0-LTS.1 and later versions.

Alarm Attributes
----------------

+-----------------------+---------------------------------+-----------------------+
| Alarm ID              | Alarm Severity                  | Auto Cleared          |
+=======================+=================================+=======================+
| 38020                 | Major (customized threshold)    | Yes                   |
|                       |                                 |                       |
|                       | Critical (customized threshold) |                       |
+-----------------------+---------------------------------+-----------------------+

Alarm Parameters
----------------

+------------------------+-------------------+----------------------------------------------------------------------+
| Type                   | Parameter         | Description                                                          |
+========================+===================+======================================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated.             |
+------------------------+-------------------+----------------------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated.             |
+------------------------+-------------------+----------------------------------------------------------------------+
|                        | TopicName         | Specifies the topic for which the alarm was generated.               |
+------------------------+-------------------+----------------------------------------------------------------------+
|                        | Alarm rule ID     | Specifies the ID of the rule corresponding to the alarm.             |
+------------------------+-------------------+----------------------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies whether the alarm is generated due to low or high traffic. |
+------------------------+-------------------+----------------------------------------------------------------------+
|                        | Info              | Specifies the actual production traffic and threshold.               |
+------------------------+-------------------+----------------------------------------------------------------------+

Impact on the System
--------------------

If the production traffic of the topics exceeds the threshold, the read and write functions of the Broker process are affected.

Possible Causes
---------------

The service traffic changes, messages are sent cyclically or repeatedly, or an abnormal branch is frequently triggered, resulting in a large number of meaningless messages or service interruption.

Handling Procedure
------------------

#. Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check details about the current alarm in the alarm list. Check the topic name of the instance for which the alarm is generated in **Location**.

#. Choose **Cluster** > **Services** > **Kafka** > **KafkaTopic Monitor** > *Topic name with the abnormal production traffic*, view the input traffic trend of the topic, and record the time segment when the production traffic changes greatly.

#. Check whether the traffic change is caused by actual service fluctuations or exceptions.

#. If the production traffic exceeds the upper limit of the threshold, determine whether to limit the production traffic of the topic based on the site requirements.

   -  If yes, go to :ref:`5 <alm-38020__en-us_topic_0000002571301739_en-us_topic_0000002525184536_li85871341184816>`.
   -  If no, go to :ref:`7 <alm-38020__en-us_topic_0000002571301739_en-us_topic_0000002525184536_li31071637131013>`.

#. .. _alm-38020__en-us_topic_0000002571301739_en-us_topic_0000002525184536_li85871341184816:

   Limit the production traffic of the topic by using a traffic control script.

   a. Log in to the node where the Kafka client is installed as the client installation user.

   b. Switch to the Kafka client installation directory, for example, **/opt/hadoopclient**.

      **cd /opt/hadoopclient**

   c. Configure environment variables.

      **source bigdata_env**

   d. Authenticate the user (skip this step for normal clusters).

      **kinit** *Component service user*

   e. Switch to the Kafka client installation directory.

      **cd Kafka/kafka**

   f. Use **kafka-configs.sh** to control the traffic of Kafka topics.

      **bin/kafka-configs.sh--zookeeper**\ *IP address of any ZooKeeper node*:*clientPort*\ **/kafka--alter--add-config** '**producer_byte_rate=**\ *Production traffic limiting speed*' **--entity-typetopics_limit--entity-name**\ *Topic name*

#. Check whether the alarm is cleared about five minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-38020__en-us_topic_0000002571301739_en-us_topic_0000002525184536_li31071637131013>`.

**Collect fault information.**

7.  .. _alm-38020__en-us_topic_0000002571301739_en-us_topic_0000002525184536_li31071637131013:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, and select **Kafka** for the target cluster.

9.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Send the collected fault logs to O&M personnel for help.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
