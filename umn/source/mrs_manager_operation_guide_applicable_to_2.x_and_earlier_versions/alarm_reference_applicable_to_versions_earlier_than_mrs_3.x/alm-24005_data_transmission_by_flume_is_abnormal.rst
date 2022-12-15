:original_name: alm_24005.html

.. _alm_24005:

ALM-24005 Data Transmission by Flume Is Abnormal
================================================

Description
-----------

The alarm module monitors the capacity of Flume channels. This alarm is generated if the duration that a channel is full or the number of times that a source fails to send data to the channel exceeds the threshold.

Users can set the threshold as required by modifying the **channelfullcount** parameter.

This alarm is cleared after the Flume channel space is released.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24005    Major          Yes
======== ============== ==========

Parameters
----------

+---------------+----------------------------------------------------------------+
| Parameter     | Description                                                    |
+===============+================================================================+
| ServiceName   | Specifies the service for which the alarm is generated.        |
+---------------+----------------------------------------------------------------+
| HostName      | Specifies the host for which the alarm is generated.           |
+---------------+----------------------------------------------------------------+
| ComponentType | Specifies the component type for which the alarm is generated. |
+---------------+----------------------------------------------------------------+
| ComponentName | Specifies the component name for which the alarm is generated. |
+---------------+----------------------------------------------------------------+

Impact on the System
--------------------

If the usage of the Flume channel continues to grow, the data transmission time increases. When the usage reaches 100%, the Flume agent process is suspended.

Possible Causes
---------------

-  The Flume sink is faulty.
-  The network is faulty.

Procedure
---------

#. Check whether the Flume sink is normal.

   a. Check whether the Flume sink is the HDFS type.

      -  If yes, go to :ref:`1.b <alm_24005__en-us_topic_0191813885_li35603802172029>`.
      -  If no, go to :ref:`1.c <alm_24005__en-us_topic_0191813885_li17206137172029>`.

   b. .. _alm_24005__en-us_topic_0191813885_li35603802172029:

      On MRS Manager, check whether the ALM-14000 HDFS Service Unavailable alarm is reported and whether the HDFS service is stopped.

      -  If the alarm is reported, clear it according to the handling suggestions of ALM-14000 HDFS Service Unavailable; if the HDFS service is stopped, start it. Then go to :ref:`1.g <alm_24005__en-us_topic_0191813885_li1487713813414>`.
      -  If no, go to :ref:`1.g <alm_24005__en-us_topic_0191813885_li1487713813414>`.

   c. .. _alm_24005__en-us_topic_0191813885_li17206137172029:

      Check whether the Flume sink is the HBase type.

      -  If yes, go to :ref:`1.d <alm_24005__en-us_topic_0191813885_li23959037172029>`.
      -  If no, go to :ref:`1.g <alm_24005__en-us_topic_0191813885_li1487713813414>`.

   d. .. _alm_24005__en-us_topic_0191813885_li23959037172029:

      On MRS Manager, check whether the ALM-19000 HBase Service Unavailable alarm is reported and whether the HBase service is stopped.

      -  If the alarm is reported, clear it according to the handling suggestions of "ALM-19000 HBase Service Unavailable"; if the HBase service is stopped, start it. Then go to :ref:`1.g <alm_24005__en-us_topic_0191813885_li1487713813414>`.
      -  If no, go to :ref:`1.g <alm_24005__en-us_topic_0191813885_li1487713813414>`.

   e. Check whether the Flume sink is the Kafka type.

      -  If yes, go to :ref:`1.f <alm_24005__en-us_topic_0191813885_li13075641172029>`.
      -  If no, go to :ref:`1.g <alm_24005__en-us_topic_0191813885_li1487713813414>`.

   f. .. _alm_24005__en-us_topic_0191813885_li13075641172029:

      On MRS Manager, check whether the ALM-38000 Kafka Service Unavailable alarm is reported and whether the Kafka service is stopped.

      -  If the alarm is reported, clear it according to the handling suggestions of "ALM-38000 Kafka Service Unavailable"; if the Kafka service is stopped, start it. Then go to :ref:`1.g <alm_24005__en-us_topic_0191813885_li1487713813414>`.
      -  If no, go to :ref:`1.g <alm_24005__en-us_topic_0191813885_li1487713813414>`.

   g. .. _alm_24005__en-us_topic_0191813885_li1487713813414:

      Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   h. Choose **Flume** > **Instances**.

   i. Click the Flume instance of the faulty node and check whether the value of the **Sink Speed Metrics** is 0.

      -  If yes, go to :ref:`2.a <alm_24005__en-us_topic_0191813885_li60707704172341>`.
      -  If no, no further action is required.

#. Check the status of the network between the Flume sink and faulty node.

   a. .. _alm_24005__en-us_topic_0191813885_li60707704172341:

      Check whether the Flume sink is the Avro type.

      -  If yes, go to :ref:`2.c <alm_24005__en-us_topic_0191813885_li31163561172341>`.
      -  If no, go to :ref:`3 <alm_24005__en-us_topic_0191813885_li572522141314>`.

   b. Log in to the host where the faulty node resides. Run the following command to switch to user **root**:

      **sudo su - root**

   c. .. _alm_24005__en-us_topic_0191813885_li31163561172341:

      Run the **ping** *Flume sink IP address* command to check whether the Flume sink can be pinged.

      -  If yes, go to :ref:`3 <alm_24005__en-us_topic_0191813885_li572522141314>`.
      -  If no, go to :ref:`2.d <alm_24005__en-us_topic_0191813885_li35581265172341>`.

   d. .. _alm_24005__en-us_topic_0191813885_li35581265172341:

      Contact the network administrator to repair the network.

   e. Wait for a while and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_24005__en-us_topic_0191813885_li572522141314>`.

#. .. _alm_24005__en-us_topic_0191813885_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
