:original_name: ALM-38001.html

.. _ALM-38001:

ALM-38001 Insufficient Kafka Disk Capacity
==========================================

Description
-----------

The system checks the Kafka disk usage every 60 seconds and compares the actual disk usage with the threshold. The disk usage has a default threshold. This alarm is generated when the disk usage is greater than the threshold.

You can change the threshold in **O&M** > **Alarm** > **Thresholds**. Under the service list, choose **Kafka > Disk > Broker Disk Usage (Broker)** and change the threshold.

When the **Trigger Count** is 1, this alarm is cleared when the Kafka disk usage is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the Kafka disk usage is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
38001    Major          Yes
======== ============== =====================

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| PartitionName     | Specifies the disk partition where the alarm is generated.                                                                   |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

Kafka data write operations are affected.

Possible Causes
---------------

-  The configuration (such as number and size) of the disks for storing Kafka data cannot meet the requirement of the current service traffic, due to which the disk usage reaches the upper limit.
-  Data retention time is too long, due to which the data disk usage reaches the upper limit.
-  The service plan does not distribute data evenly, due to which the usage of some disks reaches the upper limit.

Procedure
---------

**Check the disk configuration of Kafka data.**

#. On the FusionInsight Manager portal and click **O&M** > **Alarm** > **Alarms**.

#. .. _alm-38001__lad42a611d3f7476ebbdcc2c5b11228e3:

   In the alarm list, locate the alarm and obtain **HostName** from **Location**.

#. Click **Cluster** > *Name of the desired cluster* > **Hosts**.

#. In the host list, click the host name obtained in :ref:`2 <alm-38001__lad42a611d3f7476ebbdcc2c5b11228e3>`.

#. Check whether the **Disk** area contains the partition name in the alarm.

   -  If yes, go to :ref:`6 <alm-38001__en-us_topic_0070543586_step6a>`.
   -  If no, manually clear the alarm and no further operation is required.

#. .. _alm-38001__en-us_topic_0070543586_step6a:

   Check whether the disk partition usage contained in the alarm reaches 100% in the **Disk** area.

   -  If yes, handle the alarm by following the instructions in :ref:`Related Information <alm-38001__sc5883464b7cf4074a814e9859261a5c6>`.
   -  If no, go to :ref:`7 <alm-38001__li460742117451>`.

**Check the Kafka data storage duration.**

7.  .. _alm-38001__li460742117451:

    Choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Configurations**.

8.  Check whether the value of parameter **disk.adapter.enable** is set to **true**.

    -  If yes, go to :ref:`10 <alm-38001__li0608162194512>`.
    -  If no, go to :ref:`9 <alm-38001__li96071921164519>`.

9.  .. _alm-38001__li96071921164519:

    Set the value of **disk.adapter.enable** to **true**. Check whether the value of **adapter.topic.min.retention.hours** is properly set.

    -  If yes, go to :ref:`10 <alm-38001__li0608162194512>`.
    -  If no, adjust the data retention period based on service requirements.

    .. important::

       If the disk auto-adaptation function is enabled, some historical data of specified topics is deleted. If the retention period of some topics cannot be adjusted, click **All Configurations** and add the topics to the value of the **disk.adapter.topic.blacklist** parameter.

10. .. _alm-38001__li0608162194512:

    Wait 10 minutes and check whether the usage of faulty disks reduces.

    -  If yes, wait until the alarm is cleared.
    -  If no, go to :ref:`11 <alm-38001__li146841724812>`.

**Check the Kafka data plan.**

11. .. _alm-38001__li146841724812:

    In the **Instance** area, click **Broker**. In the **Real Time** area of Broker, Click the drop-down menu in the Chart area and choose **Customize** to customize monitoring items.

12. .. _alm-38001__li1681217164815:

    In the dialog box, select **Disk** > **Broker Disk Usage** and click **OK**.

    The Kafka disk usage information is displayed.

13. View the information in :ref:`12 <alm-38001__li1681217164815>` to check whether there is only the disk parathion for which the alarm is generated in :ref:`2 <alm-38001__lad42a611d3f7476ebbdcc2c5b11228e3>`.

    -  If yes, go to :ref:`14 <alm-38001__li76811719488>`.
    -  If no, go to :ref:`15 <alm-38001__li4681517154817>`.

14. .. _alm-38001__li76811719488:

    Perform disk planning and mount a new disk again. Go to the **Instance Configurations** page of the node for which the alarm is generated, modify **log.dirs**, add other disk directories, and restart the Kafka instance.

15. .. _alm-38001__li4681517154817:

    Determine whether to shorten the data retention time configured on Kafka based on service requirements and service traffic.

    -  If yes, go to :ref:`16 <alm-38001__li3691217164814>`.
    -  If no, go to :ref:`17 <alm-38001__li86921715482>`.

16. .. _alm-38001__li3691217164814:

    Log in to FusionInsight Manager, select **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Configurations**, and click **All Configurations**. In the search box on the right, enter **log.retention.hours**. The value of the parameter indicates the default data retention time of the topic. You can change the value to a smaller one.

    .. note::

       -  For a topic whose data retention time is configured alone, the modification of the data retention time on the Kafka Service Configuration page does not take effect.

       -  To modify the data retention time for a topic, use the Kafka client command-line interface (CLI) to configure the topic.

          Example: **kafka-topics.sh --zookeeper "**\ *ZooKeeper IP address*\ **:2181/kafka" --alter --topic "**\ *Topic bane*\ **" --config retention.ms= "**\ *retention time*\ **"**

17. .. _alm-38001__li86921715482:

    Check whether the usage of some disks reaches the upper limit due to unreasonable configuration of the partitions of some topics. For example, the number of partitions configured for a topic with large data volume is smaller than the number of disks. In this case, the data is not evenly allocated to disks.

    .. note::

       If you do not know which topic has large data volume, you can log in to an instance node based on the host node information obtained in :ref:`2 <alm-38001__lad42a611d3f7476ebbdcc2c5b11228e3>`, and go to the data directory (directory specified by **log.dirs** before the modification in :ref:`14 <alm-38001__li76811719488>`) to check whether there is topic with partition that use large disk space.

    -  If yes, go to :ref:`18 <alm-38001__li106991718484>`.
    -  If no, go to :ref:`19 <alm-38001__li6701817194816>`.

18. .. _alm-38001__li106991718484:

    In the Kafka client CLI, run the following command to perform partition capacity expansion for the topic:

    **kafka-topics.sh --zookeeper "**\ *ZooKeeper IP address*\ **:2181/kafka" --alter --topic "**\ *Topic name*\ **" --partitions="**\ *New number of partitions*\ **"**

    .. note::

       -  You are advised to set the new number of partitions to a multiple of the number of Kafka data disks.
       -  The step may not quickly clear the alarm, and you need to modify the data retention time in :ref:`11 <alm-38001__li146841724812>` to gradually balance data allocation.

19. .. _alm-38001__li6701817194816:

    Determine whether to perform capacity expansion.

    .. note::

       You are advised to perform capacity expansion for Kafka when the current disk usage exceeds 80%.

    -  If yes, go to :ref:`20 <alm-38001__li1670517124811>`.
    -  If no, go to :ref:`21 <alm-38001__li1170111717488>`.

20. .. _alm-38001__li1670517124811:

    Expand the disk capacity and check whether the alarm is cleared after capacity expansion.

    -  If yes, no further action is required.
    -  If no, go to :ref:`22 <alm-38001__li1311215881510>`.

21. .. _alm-38001__li1170111717488:

    Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`22 <alm-38001__li1311215881510>`.

**Collect fault information.**

22. .. _alm-38001__li1311215881510:

    On the FusionInsight Manager portal, choose **O&M** > **Log** > **Download**.

23. Select **Kafka** in the required cluster from the **Service** drop-down list.

24. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

25. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

.. _alm-38001__sc5883464b7cf4074a814e9859261a5c6:

Related Information
-------------------

#. Log in to FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Instance**, stop the Broker instance whose status is **Restoring**, record the management IP address of the node where the Broker instance is located, and record **broker.id**. The value can be obtained by using the following method: Click the role name. On the **Configurations** page, select **All Configurations**, and search for the **broker.id** parameter.

#. Log in to the recorded management IP address as user **root**, and run the **df -lh** command to view the mounted directory whose disk usage is 100%, for example, **${BIGDATA_DATA_HOME}/kafka/data1**.

#. Go to the directory, run the **du -sh \*** command to view the size of each file in the directory,check whether files other than **kafka-logs** exist, and determine whether these files can be deleted or migrated.

   -  If yes, go to :ref:`8 <alm-38001__le5f408260b7c4eaea839d9f216e3039b>`.
   -  If no, go to :ref:`4 <alm-38001__l6b4a3aa101714691aebfd7f69ccfc8d4>`.

#. .. _alm-38001__l6b4a3aa101714691aebfd7f69ccfc8d4:

   Go to the **kafka-logs** directory, run the **du -sh \*** command, select a partition folder to be moved. The naming rule is **Topic name-Partition ID**. Record the topic and partition.

#. .. _alm-38001__l847204e787034666b0ffc45eaaaf2cd4:

   Modify the **recovery-point-offset-checkpoint** and **replication-offset-checkpoint** files in the **kafka-logs** directory in the same way.

   a. Decrease the number in the second line in the file. (To remove multiple directories, the number deducted is equal to the number of files to be removed.)
   b. Delete the line of the to-be-removed partition. (The line structure is "Topic name Partition ID Offset". Save the data before deletion. Subsequently, the content must be added to the file of the same name in the destination directory.)

#. Modify the **recovery-point-offset-checkpoint** and **replication-offset-checkpoint** files in the destination data directory. For example, **${BIGDATA_DATA_HOME}/kafka/data2/kafka-logs** in the same way.

   -  Increase the number in the second line in the file. (To move multiple directories, the number added is equal to the number of files to be moved.)
   -  Add the to-be moved partition to the end of the file. (The line structure is "Topic name Partition ID Offset". You can copy the line data saved in :ref:`5 <alm-38001__l847204e787034666b0ffc45eaaaf2cd4>`.)

#. Move the partition to the destination directory. After the partition is moved, run the **chown omm:wheel -R** *Partition directory* command to modify the directory owner group for the partition.

#. .. _alm-38001__le5f408260b7c4eaea839d9f216e3039b:

   Log in to FusionInsight Manager and choose **Cluster** > *Name of the desired cluster* > **Services** > **Kafka** > **Instance** to start the Broker instance.

#. Wait for 5 to 10 minutes and check whether the health status of the Broker instance is **Normal**.

   -  If yes, resolve the disk capacity insufficiency problem according to the handling method of "ALM-38001 Insufficient Kafka Disk Space" after the alarm is cleared.
   -  If no, contact the O&M personnel.

.. |image1| image:: /_static/images/en-us_image_0000001532607862.png
