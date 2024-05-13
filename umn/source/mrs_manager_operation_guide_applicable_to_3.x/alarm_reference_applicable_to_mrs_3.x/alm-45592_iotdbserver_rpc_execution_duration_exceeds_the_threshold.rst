:original_name: ALM-45592.html

.. _ALM-45592:

ALM-45592 IoTDBServer RPC Execution Duration Exceeds the Threshold
==================================================================

Description
-----------

The system checks the RPC execution duration of the IoTDBServer process every 60 seconds. This alarm is generated when the execution duration exceeds the threshold. This alarm is cleared when the RPC execution time of the IoTDBServer process is less than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45592    Major          Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

Running performance of the IoTDBServer process is affected.

Possible Causes
---------------

The processing duration of an IoTDBServer RPC request exceeds the threshold. Logs need to be further analyzed to locate the cause.

Procedure
---------

**Collect fault information.**

#. .. _alm-45592__li17507311599:

   Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the real-time alarm list, click |image1| in front of this alarm and view the role name and instance IP address in **Location**.

#. Choose **O&M** > **Log** > **Download**.

#. Expand the **Service** drop-down list, select **IoTDB** for the target cluster, and click **OK**.

#. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the host queried in :ref:`1 <alm-45592__li17507311599>`, and click **OK**.

#. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

#. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583087297.png
.. |image2| image:: /_static/images/en-us_image_0000001532448158.png
