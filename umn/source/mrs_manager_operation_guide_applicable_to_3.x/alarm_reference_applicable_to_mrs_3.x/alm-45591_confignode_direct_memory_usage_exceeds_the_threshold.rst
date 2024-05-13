:original_name: ALM-45591.html

.. _ALM-45591:

ALM-45591 ConfigNode Direct Memory Usage Exceeds the Threshold
==============================================================

Description
-----------

The system checks the direct memory usage of the ConfigNode process every 60 seconds. This alarm is generated when the direct memory usage of the ConfigNode exceeds the threshold for five consecutive times. That is, the direct memory configured for ConfigNode cannot meet service requirements. This alarm is cleared when the direct memory usage of ConfigNode is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45591    Major          Yes
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

Direct memory overflow may cause the IoTDB instance to be unavailable.

Possible Causes
---------------

The direct memory configured for the node is improper. As a result, the usage exceeds the threshold.

Procedure
---------

**Check the direct memory configuration.**

#. .. _alm-45591__li823572385459:

   Log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**. In the real-time alarm list, click |image1| in front of this alarm and view the role name and instance IP address in **Location**.

#. Choose **Cluster** > **Services** > **IoTDB**. Click **Instance**, click the ConfigNode corresponding to the IP address obtained in :ref:`1 <alm-45591__li823572385459>`, and check whether **ConfigNode Direct Memory Usage** on the **Dashboard** tab page reaches the threshold specified for the ConfigNode process (90% of the maximum direct memory by default).

   If the chart is not displayed, click the drop-down list in the upper right corner of the chart area and choose **Customize** > **Memory**. In the dialog box that is displayed, select **ConfigNode Direct Memory Usage** and click **OK**.

   -  If yes, go to :ref:`3 <alm-45591__li10450762161055>`.
   -  If no, go to :ref:`5 <alm-45591__d0e43963>`.

#. .. _alm-45591__li10450762161055:

   On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **IoTDB**. Click **Configurations** then **All Configurations**. Click **ConfigNode** and select **System**. Set **-XX:MaxDirectMemorySize** in **GC_OPTS** to a larger value as required and save the configuration.

   .. note::

      -  You are advised to set **-XX:MaxDirectMemorySize** in **GC_OPTS** to twice the direct memory used by the ConfigNode process. (You can change the value based on the actual service scenario.)
      -  To obtain the size of the direct memory used by the ConfigNode process, choose **Customize** > **Memory** > **ConfigNode Direct Memory Resource Status**.
      -  If **GC_OPTS** does not contain the **-XX:MaxDirectMemorySize** parameter, add it.

#. Restart the affected IoTDB service or instances and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45591__d0e43963>`.

**Collect fault information.**

5. .. _alm-45591__d0e43963:

   On MRS Manager, choose **O&M** > **Log** > **Download**.

6. Expand the **Service** drop-down list, and select **ConfigNode** for the destination cluster.

7. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the hosts to which the role belongs, and click **OK**.

8. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583127501.png
.. |image2| image:: /_static/images/en-us_image_0000001582807809.png
