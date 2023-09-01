:original_name: ALM-45589.html

.. _ALM-45589:

ALM-45589 ConfigNode Heap Memory Usage Exceeds the Threshold
============================================================

Description
-----------

The system checks the heap memory usage of the ConfigNode process every 60 seconds. This alarm is generated when the heap memory usage of the ConfigNode process exceeds the threshold (90% of the maximum memory). This alarm is cleared when the heap memory usage of the ConfigNode process is less than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45589    Major          Yes
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

If the heap memory usage of the ConfigNode process is too high, the performance of the ConfigNode process is affected, and even the ConfigNode process becomes unavailable due to memory overflow.

Possible Causes
---------------

The heap memory configured for the node is improper. As a result, the usage exceeds the threshold.

Procedure
---------

**Check the heap memory configuration.**

#. .. _alm-45589__li823572385459:

   Log in to FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**. In the real-time alarm list, click |image1| in front of this alarm and view the role name and instance IP address in **Location**.

#. Choose **Cluster** > **Services** > **IoTDB**. Click **Instance**, click the ConfigNode corresponding to the IP address obtained in :ref:`1 <alm-45589__li823572385459>`, and check whether **ConfigNode Heap Memory Usage** on the **Dashboard** tab page reaches the threshold specified for the ConfigNode process.

   If the chart is not displayed, click the drop-down list in the upper right corner of the chart area and choose **Customize** > **Memory**. In the dialog box that is displayed, select **ConfigNode Heap Memory Usage** and click **OK**.

   .. note::

      You can choose **O&M** > **Alarm** > **Threshold Configuration** > *Name of the desired cluster* > **IoTDB** > **Memory** > **ConfigNode Heap Memory Usage (ConfigNode)** to view the threshold.

   -  If yes, go to :ref:`3 <alm-45589__li1141514131368>`.
   -  If no, go to :ref:`6 <alm-45589__li122373616176>`.

#. .. _alm-45589__li1141514131368:

   Choose **Cluster** > **Services** > **IoTDB**. Click **Configurations** then **All Configurations**, click **ConfigNode**, and choose **System**. Set **-Xmx** in **GC_OPTS** to a larger value and save the configuration.

   .. note::

      -  The default value of -**Xmx** is **2G**.
      -  If this alarm is occasionally generated, increase the value of **-Xmx** by 0.5 times. If this alarm is frequently generated, double the value of **-Xmx**.
      -  In the case of large service volume and high service concurrency, you are advised to add instances.

#. Click **Dashboard**. Click **Restart Service** to restart the IoTDB service for the configuration to take effect.

#. Wait for about 120 seconds and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45589__li122373616176>`.

**Collect fault information.**

6.  .. _alm-45589__li122373616176:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

7.  Expand the **Service** drop-down list, select **IoTDB** for the target cluster, and click **OK**.

8.  Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the hosts to which the role belongs, and click **OK**.

9.  Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807589.png
.. |image2| image:: /_static/images/en-us_image_0000001532607642.png
