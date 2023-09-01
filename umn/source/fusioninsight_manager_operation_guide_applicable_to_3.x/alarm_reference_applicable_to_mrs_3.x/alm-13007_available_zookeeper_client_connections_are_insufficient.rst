:original_name: ALM-13007.html

.. _ALM-13007:

ALM-13007 Available ZooKeeper Client Connections Are Insufficient
=================================================================

Description
-----------

The system periodically detects the number of active processes between the ZooKeeper client and the ZooKeeper server every 60 seconds. This alarm is generated when the number of connections exceeds the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
13007    Minor          Yes
======== ============== =====================

Parameters
----------

+-------------------+--------------------------------------------------------------+
| Name              | Meaning                                                      |
+===================+==============================================================+
| Source            | Specifies the cluster for which the alarm is generated.      |
+-------------------+--------------------------------------------------------------+
| ServiceName       | Specifies the service name for which the alarm is generated. |
+-------------------+--------------------------------------------------------------+
| RoleName          | Specifies the role name for which the alarm is generated.    |
+-------------------+--------------------------------------------------------------+
| HostName          | Specifies the host name for which the alarm is generated.    |
+-------------------+--------------------------------------------------------------+
| ClientIP          | Specifies the client IP address.                             |
+-------------------+--------------------------------------------------------------+
| ServerIP          | Specifies the server IP address.                             |
+-------------------+--------------------------------------------------------------+
| Trigger Condition | Specifies the cause of the alarm.                            |
+-------------------+--------------------------------------------------------------+

Impact on the System
--------------------

A large number of connections to ZooKeeper caused the ZooKeeper to be fully connected and unable to provide normal services.

Possible Causes
---------------

A large number of client processes are connected to ZooKeeper. The thresholds are not appropriate.

Procedure
---------

**Check whether there are a large number of client processes connected to ZooKeeper.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**. On the displayed interface, click the drop-down button of **Available ZooKeeper Client Connections Are Insufficient**. Confirm the node IP address of the host for which the alarm is generated in the Location Information.

#. Open the ZooKeeper service interface, click **Resource** to enter the **Resource** page, and check whether the number of connections of the client with the IP address specified by **Number of Connections** **(By Client IP Address)** is large.

   -  If it is, go to :ref:`3 <alm-13007__li9739531132620>`.
   -  If it is not, go to :ref:`4 <alm-13007__li1373973122619>`.

#. .. _alm-13007__li9739531132620:

   Check whether connection leakage occurs on the client process.

#. .. _alm-13007__li1373973122619:

   Click\ |image1| in the **Number of Connections** **(by Client IP Address)** to enter the **Thresholds** page, and click **Modify** under **Operation**. Increase the threshold by referring to the value of **maxClientCnxns** by choosing **Cluster >** *Name of the desired cluster* **> Services** > **ZooKeeper** > **Configurations > All Configurations > quorumpeer**.

#. Check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`6 <alm-13007__li27361331112613>`.

**Collect fault information.**

6. .. _alm-13007__li27361331112613:

   On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

7. Select **ZooKeeper** in the required cluster from the **Service**.

8. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767466.gif
.. |image2| image:: /_static/images/en-us_image_0000001532927402.png
