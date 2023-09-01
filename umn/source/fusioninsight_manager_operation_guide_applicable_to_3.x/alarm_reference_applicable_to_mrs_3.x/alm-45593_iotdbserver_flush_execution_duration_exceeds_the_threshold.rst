:original_name: ALM-45593.html

.. _ALM-45593:

ALM-45593 IoTDBServer Flush Execution Duration Exceeds the Threshold
====================================================================

Description
-----------

This alarm is generated when the data flush duration exceeds the threshold. This alarm is cleared when the flush duration is less than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45593    Major          Yes
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

Data write is blocked and the write operation performance is affected.

Possible Causes
---------------

The IoTDB flushing on the node is slow. You need to further analyze logs.

Procedure
---------

**Collect fault information.**

#. .. _alm-45593__li7938175019120:

   Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**. In the real-time alarm list, click |image1| in front of this alarm and view the role name and instance IP address in **Location**.

#. Choose **O&M** > **Log** > **Download**.

#. Expand the **Service** drop-down list, select **IoTDB** for the target cluster, and click **OK**.

#. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the host queried in :ref:`1 <alm-45593__li7938175019120>`, and click **OK**.

#. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

#. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607638.png
.. |image2| image:: /_static/images/en-us_image_0000001532767370.png
