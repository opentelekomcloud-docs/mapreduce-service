:original_name: alm_24004.html

.. _alm_24004:

ALM-24004 Flume Fails to Read Data
==================================

Description
-----------

The alarm module monitors the Flume source status. This alarm is generated if the duration that Flume source fails to read data exceeds the threshold.

Users can modify the threshold as required.

This alarm is cleared if the source reads data successfully.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24004    Major          Yes
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

Data collection is stopped.

Possible Causes
---------------

-  The Flume source is faulty.
-  The network is faulty.

Procedure
---------

#. Check whether the Flume source is normal.

   a. Check whether the Flume source is the spoolDir type.

      -  If yes, go to :ref:`1.b <alm_24004__en-us_topic_0191813945_li57424576173633>`.
      -  If no, go to :ref:`1.c <alm_24004__en-us_topic_0191813945_li27889489173633>`.

   b. .. _alm_24004__en-us_topic_0191813945_li57424576173633:

      Query the **spoolDir** directory and check whether all files have been sent.

      -  If yes, no further action is required.
      -  If no, go to :ref:`1.e <alm_24004__en-us_topic_0191813945_li1487713813414>`.

   c. .. _alm_24004__en-us_topic_0191813945_li27889489173633:

      Check whether the Flume source is the Kafka type.

      -  If yes, go to :ref:`1.d <alm_24004__en-us_topic_0191813945_li35944619173633>`.
      -  If no, go to :ref:`1.e <alm_24004__en-us_topic_0191813945_li1487713813414>`.

   d. .. _alm_24004__en-us_topic_0191813945_li35944619173633:

      Log in to the Kafka client and run the following commands to check whether all topic data configured for the Kafka source has been consumed.

      **cd /opt/client/Kafka/kafka/bin**

      **./kafka-consumer-groups.sh --bootstrap-server** *Kafka cluster IP address*\ **:21007** **--new-consumer --describe --group example-group1 --command-config**

      **../config/consumer.properties**

      -  If yes, no further action is required.
      -  If no, go to :ref:`1.e <alm_24004__en-us_topic_0191813945_li1487713813414>`.

   e. .. _alm_24004__en-us_topic_0191813945_li1487713813414:

      Go to the cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   f. Choose **Flume** > **Instances**.

   g. Click the Flume instance of the faulty node and check whether the value of the **Source Speed Metrics** is 0.

      -  If yes, go to :ref:`2.a <alm_24004__en-us_topic_0191813945_li39514043173729>`.
      -  If no, no further action is required.

#. Check the status of the network between the Flume source and faulty node.

   a. .. _alm_24004__en-us_topic_0191813945_li39514043173729:

      Check whether the Flume source is the avro type.

      -  If yes, go to :ref:`2.c <alm_24004__en-us_topic_0191813945_li52369777173729>`.
      -  If no, go to :ref:`3 <alm_24004__en-us_topic_0191813945_li572522141314>`.

   b. Log in to the host where the faulty node resides. Run the following command to switch to user **root**:

      **sudo su - root**

   c. .. _alm_24004__en-us_topic_0191813945_li52369777173729:

      Run the **ping** *Flume source IP address* command to check whether the Flume source can be pinged.

      -  If yes, go to :ref:`3 <alm_24004__en-us_topic_0191813945_li572522141314>`.
      -  If no, go to :ref:`2.d <alm_24004__en-us_topic_0191813945_li27478632173729>`.

   d. .. _alm_24004__en-us_topic_0191813945_li27478632173729:

      Contact the network administrator to repair the network.

   e. Wait for a while and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_24004__en-us_topic_0191813945_li572522141314>`.

#. .. _alm_24004__en-us_topic_0191813945_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
