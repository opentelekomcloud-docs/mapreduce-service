:original_name: ALM-45590.html

.. _ALM-45590:

ALM-45590 ConfigNode GC Duration Exceeds the Threshold
======================================================

Description
-----------

The system checks the GC duration of the ConfigNode process every 60 seconds. This alarm is generated when the GC duration exceeds the threshold (12 seconds by default) for three consecutive times. This alarm is cleared when the GC duration is less than the threshold.

.. note::

   You can choose **O&M** > **Alarm** > **Threshold Configuration** > *Name of the desired cluster* > **IoTDB** > **GC** > **Total GC duration of ConfigNode process (ConfigNode)** to increase the threshold by 20% each time.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45590    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+---------------------------------------------------------+
| Name              | Meaning                                                 |
+===================+=========================================================+
| Source            | Specifies the cluster for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.       |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

A long GC duration of the ConfigNode process may interrupt services.

Possible Causes
---------------

The heap memory configured on the node is improper. As a result, GC occurs frequently.

Procedure
---------

**Check the heap memory configuration.**

#. .. _alm-45590__li823572385459:

   Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the real-time alarm list, click |image1| in the row containing this alarm and view the role name and instance IP address in **Location**.

#. Choose **Cluster** > **Services** > **IoTDB**. Click **Instance**, click the ConfigNode corresponding to the IP address obtained by :ref:`1 <alm-45590__li823572385459>`. Switch to the **Dashboard** tab page, locate the **Total GC Duration of ConfigNode** chart, and check whether the GC duration of the ConfigNode process exceeds the threshold.

   If the GC duration of ConfigNode is not displayed, click the drop-down list in the upper right corner of the chart area and choose **Customize** > **GC**. In the displayed dialog box, select **Total GC Duration of ConfigNode** and click **OK**.

   .. note::

      You can choose **O&M** > **Alarm** > **Threshold Configuration** > *Name of the desired cluster* > **IoTDB** > **GC** > **Total GC duration of ConfigNode process (ConfigNode)** to view the threshold.

   -  If yes, go to :ref:`3 <alm-45590__li1141514131368>`.
   -  If no, go to :ref:`6 <alm-45590__li4749473185459>`.

#. .. _alm-45590__li1141514131368:

   Choose **Cluster** > **Services** > **IoTDB**. Click **Configurations** then **All Configurations**, click **ConfigNode**, and choose **System**. Set **-Xmx** in **GC_OPTS** to a larger value and save the configuration.

   .. note::

      -  The default value of -**Xmx** is **2G**.
      -  If this alarm is occasionally generated, increase the value by 0.5 times. If this alarm is frequently generated, double the value.
      -  In the case of large service volume and high service concurrency, you are advised to add instances.

#. Click **Dashboard**. Click **Restart Service** to restart the IoTDB service for the configuration to take effect.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-45590__li4749473185459>`.

**Collect fault information.**

6.  .. _alm-45590__li4749473185459:

    On MRS Manager, choose **O&M** > **Log** > **Download**.

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

.. |image1| image:: /_static/images/en-us_image_0000001532448138.png
.. |image2| image:: /_static/images/en-us_image_0000001582807569.png
