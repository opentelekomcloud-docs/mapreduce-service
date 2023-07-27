:original_name: ALM-24005.html

.. _ALM-24005:

ALM-24005 Exception Occurs When Flume Transmits Data
====================================================

Description
-----------

The alarm module monitors the capacity status of Flume Channel. The alarm is generated immediately when the duration that Channel is fully occupied exceeds the threshold or the number of times that Source fails to send data to Channel exceeds the threshold.

The default threshold is **10**. You can change the threshold by modifying the **channelfullcount** parameter of the related channel in the **properties.properties** configuration file in the **conf** directory.

The alarm is cleared when the space of Flume Channel is released and the alarm handling is complete.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24005    Major          Yes
======== ============== ==========

Parameters
----------

+---------------+-----------------------------------------------------------------------+
| Name          | Meaning                                                               |
+===============+=======================================================================+
| Source        | Specifies the cluster for which the alarm is generated.               |
+---------------+-----------------------------------------------------------------------+
| ServiceName   | Specifies the service for which the alarm is generated.               |
+---------------+-----------------------------------------------------------------------+
| HostName      | Specifies the host for which the alarm is generated.                  |
+---------------+-----------------------------------------------------------------------+
| AgentId       | Specifies the ID of the agent for which the alarm is generated.       |
+---------------+-----------------------------------------------------------------------+
| ComponentType | Specifies the type of the component for which the alarm is generated. |
+---------------+-----------------------------------------------------------------------+
| ComponentName | Specifies the component for which the alarm is generated.             |
+---------------+-----------------------------------------------------------------------+

Impact on the System
--------------------

If the disk usage of Flume Channel increases continuously, the time required for importing data to a specified destination prolongs. When the disk usage of Flume Channel reaches 100%, the Flume agent process pauses.

Possible Causes
---------------

-  Flume Sink is faulty, so the data cannot be sent.
-  The network is faulty, so the data cannot be sent.

Procedure
---------

**Check whether Flume Sink is faulty.**

#. Open the **properties.properties** configuration file on the local PC, search for **type = hdfs** in the file, and check whether the Flume sink type is HDFS.

   -  If yes, go to :ref:`2 <alm-24005__li893062611148>`.
   -  If no, go to :ref:`3 <alm-24005__li2804053511148>`.

#. .. _alm-24005__li893062611148:

   On FusionInsight Manager, check whether **HDFS Service Unavailable** alarm is generated in the alarm list and whether the HDFS service is stopped in the service list.

   -  If the alarm is reported, clear it according to the handling suggestions of ALM-14000 HDFS Service Unavailable; if the HDFS service is stopped, start it. Then, go to :ref:`7 <alm-24005__li5165783111148>`.
   -  If no, go to :ref:`7 <alm-24005__li5165783111148>`.

#. .. _alm-24005__li2804053511148:

   Open the **properties.properties** configuration file on the local PC, search for **type = hbase** in the file, and check whether the Flume sink type is HBase.

   -  If yes, go to :ref:`4 <alm-24005__li5423421711148>`.
   -  If no, go to :ref:`5 <alm-24005__li3655261711148>`.

#. .. _alm-24005__li5423421711148:

   On FusionInsight Manager, check whether **HBase Service Unavailable** alarm is generated in the alarm list and whether the HBase service is stopped in the service list.

   -  If the alarm is reported, clear it according to the handling suggestions of ALM-19000 HBase Service Unavailable; if the HBase service is stopped, start it. Then, go to :ref:`7 <alm-24005__li5165783111148>`.
   -  If no, go to :ref:`7 <alm-24005__li5165783111148>`.

#. .. _alm-24005__li3655261711148:

   Open the **properties.properties** configuration file on the local PC, search for **org.apache.flume.sink.kafka.KafkaSink** in the file, and check whether the Flume sink type is Kafka.

   -  If yes, go to :ref:`6 <alm-24005__li5047900111148>`.
   -  If no, go to :ref:`9 <alm-24005__li3789323111148>`.

#. .. _alm-24005__li5047900111148:

   On FusionInsight Manager, check whether **Kafka Service Unavailable** alarm is generated in the alarm list and whether the Kafka service is stopped in the service list.

   -  If the alarm is reported, clear it according to the handling suggestions of ALM-38000 Kafka Service Unavailable; if the Kafka service is stopped, start it. Then, go to :ref:`7 <alm-24005__li5165783111148>`.
   -  If no, go to :ref:`7 <alm-24005__li5165783111148>`.

#. .. _alm-24005__li5165783111148:

   On FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Flume** > **Instance**.

#. Go to the Flume instance page of the faulty node to check whether the indicator **Sink Speed Metrics** is 0.

   -  If yes, go to :ref:`13 <alm-24005__li2555818811148>`.
   -  If no, go to :ref:`9 <alm-24005__li3789323111148>`.

**Check the network connection between the faulty node and the node that corresponds to the Flume Sink IP address.**

9.  .. _alm-24005__li3789323111148:

    Open the **properties.properties** configuration file on the local PC, search for **type = avro** in the file, and check whether the Flume sink type is Avro.

    -  If yes, go to :ref:`10 <alm-24005__li3657487511148>`.
    -  If no, go to :ref:`13 <alm-24005__li2555818811148>`.

10. .. _alm-24005__li3657487511148:

    Log in to the faulty node as user **root**, and run the **ping** *IP address of the Flume sink* command to check whether the peer host can be pinged successfully.

    -  If yes, go to :ref:`13 <alm-24005__li2555818811148>`.
    -  If no, go to :ref:`11 <alm-24005__li6073842411148>`.

11. .. _alm-24005__li6073842411148:

    Contact the network administrator to restore the network.

12. In the alarm list, check whether the alarm is cleared after a period.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-24005__li2555818811148>`.

**Collect the fault information.**

13. .. _alm-24005__li2555818811148:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

14. Expand the **Service** drop-down list, and select **Flume** for the target cluster.

15. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767398.png
