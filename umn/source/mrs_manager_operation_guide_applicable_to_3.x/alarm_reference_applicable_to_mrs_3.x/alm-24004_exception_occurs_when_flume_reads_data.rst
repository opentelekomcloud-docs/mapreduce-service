:original_name: ALM-24004.html

.. _ALM-24004:

ALM-24004 Exception Occurs When Flume Reads Data
================================================

Description
-----------

The alarm module monitors the status of Flume Source. This alarm is generated immediately when the duration in which Source fails to read the data exceeds the threshold.

The default threshold is **0**, indicating that the threshold is disabled. You can change the threshold by modifying the **properties.properties** file in the **conf** directory. Specifically, modify the **NoDatatime** parameter of required the source.

The alarm is cleared when Source reads the data and the alarm handling is complete.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
24004    Major          Yes
======== ============== ==========

Parameters
----------

+---------------+-----------------------------------------------------------------+
| Name          | Meaning                                                         |
+===============+=================================================================+
| Source        | Specifies the cluster for which the alarm is generated.         |
+---------------+-----------------------------------------------------------------+
| ServiceName   | Specifies the service for which the alarm is generated.         |
+---------------+-----------------------------------------------------------------+
| HostName      | Specifies the host for which the alarm is generated.            |
+---------------+-----------------------------------------------------------------+
| AgentId       | Specifies the ID of the agent for which the alarm is generated. |
+---------------+-----------------------------------------------------------------+
| ComponentType | Specifies the component type for which the alarm is generated.  |
+---------------+-----------------------------------------------------------------+
| ComponentName | Specifies the component name for which the alarm is generated.  |
+---------------+-----------------------------------------------------------------+

Impact on the System
--------------------

If data is found in the data source and Flume Source continuously fails to read data, the data collection is stopped.

Possible Causes
---------------

-  Flume Source is faulty, so data cannot be sent.
-  The network is faulty, so the data cannot be sent.

Procedure
---------

**Check whether Flume Source is faulty.**

#. Open the **properties.properties** configuration file on the local PC, search for **keyword type = spooldir** in the file, and check whether the Flume source type is spoolDir.

   -  If yes, go to :ref:`2 <alm-24004__li3561010711655>`.
   -  If no, go to :ref:`3 <alm-24004__li3862672011655>`.

#. .. _alm-24004__li3561010711655:

   View the spoolDir directory to check whether all files are already transferred.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-24004__li2692021011655>`.

      .. note::

         The monitoring directory of spooDir is specified by the **.spoolDir** parameter in the **properties.properties** configuration file. If all files in the monitoring directory have been transferred, the file name extension of all files in the monitoring directory is **.COMPLETED**.

#. .. _alm-24004__li3862672011655:

   Open the **properties.properties** configuration file on the local PC, search for **org.apache.flume.source.kafka.KafkaSource** in the file, and check whether the Flume source type is Kafka.

   -  If yes, go to :ref:`4 <alm-24004__li4027383611655>`.
   -  If no, go to :ref:`7 <alm-24004__li5944850711655>`.

#. .. _alm-24004__li4027383611655:

   Check whether the topic data configured by Kafka Source has been used up.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-24004__li2692021011655>`.

#. .. _alm-24004__li2692021011655:

   On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Flume** > **Instance**.

#. Go to the Flume instance page of the faulty node to check whether the indicator **Source Speed Metrics** in the alarm is 0.

   -  If yes, go to :ref:`11 <alm-24004__li1313046711655>`.
   -  If no, go to :ref:`7 <alm-24004__li5944850711655>`.

**Check the network connection between the faulty node and the node that corresponds to the Flume Source IP address.**

7.  .. _alm-24004__li5944850711655:

    Open the **properties.properties** configuration file on the local PC, search for **type = avro** in the file, and check whether the Flume source type is Avro.

    -  If yes, go to :ref:`8 <alm-24004__li6550564111655>`.
    -  If no, go to :ref:`11 <alm-24004__li1313046711655>`.

8.  .. _alm-24004__li6550564111655:

    Log in to the faulty node as user **root**, and run the **ping** *IP address of the Flume source* command to check whether the peer host can be pinged successfully.

    -  If yes, go to :ref:`11 <alm-24004__li1313046711655>`.
    -  If no, go to :ref:`9 <alm-24004__li5267986211655>`.

9.  .. _alm-24004__li5267986211655:

    Contact the network administrator to restore the network.

10. In the alarm list, check whether the alarm is cleared after a period.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-24004__li1313046711655>`.

**Collect the fault information.**

11. .. _alm-24004__li1313046711655:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

12. Expand the **Service** drop-down list, and select **Flume** for the target cluster.

13. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927554.png
