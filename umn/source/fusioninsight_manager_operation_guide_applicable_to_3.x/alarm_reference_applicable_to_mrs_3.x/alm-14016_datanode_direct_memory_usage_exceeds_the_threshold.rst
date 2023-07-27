:original_name: ALM-14016.html

.. _ALM-14016:

ALM-14016 DataNode Direct Memory Usage Exceeds the Threshold
============================================================

Description
-----------

The system checks the direct memory usage of HDFS every 30 seconds. This alarm is generated when the direct memory usage of DataNode instances exceeds the threshold (90% of the maximum memory).

This alarm is automatically cleared when the direct memory usage is less than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
14016    Major          Yes
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

If the available direct memory of DataNode instances is insufficient, a memory overflow may occur and the service breaks down.

Possible Causes
---------------

The direct memory of DataNode instances is overused or the direct memory is inappropriately allocated.

Procedure
---------

**Check the direct memory usage.**

#. On the **Home** page of FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**. On the page that is displayed, click the drop-down list in the row containing **ALM-14016 DataNode Direct Memory Usage Exceeds the Threshold**, and view the role name and IP address of the instance for which the alarm is generated in the **Location** area.

#. On the **Home** page of FusionInsight Manager, choose **Cluster** > **Services** > **HDFS**. On the page that is displayed, click the **Instance** tab. In the instance list, select **DataNode** (IP address of the instance for which this alarm is generated). Click the drop-down list in the upper right corner of the chart, choose **Customize** > **Resource**, and select **DataNode Memory** to check the direct memory usage.

#. Check whether the used direct memory of a DataNode instance reaches 90% (default threshold) of the maximum direct memory allocated to it.

   -  If yes, go to :ref:`4 <alm-14016__li3399087993722>`.
   -  If no, go to :ref:`8 <alm-14016__li5838381193722>`.

#. .. _alm-14016__li3399087993722:

   On the **Home** page of FusionInsight Manager, choose **Cluster** > **Services** > **HDFS**. On the page that is displayed, click the **Configuration** tab then the **All Configurations** sub-tab, and select **DataNode** > **System**. Check whether **-XX:MaxDirectMemorySize** exists in the **GC_OPTS** parameter.

   -  If yes, go to :ref:`5 <alm-14016__li062164310159>`.
   -  If no, go to :ref:`6 <alm-14016__li111010376180>`.

#. .. _alm-14016__li062164310159:

   Adjust the value of **-XX:MaxDirectMemorySize**.

   a. In **GC_OPTS**, check the value of **-Xmx** and check whether the node memory is sufficient.

      .. note::

         You can determine whether the node memory is sufficient based on the actual environment. For example, you can use the following method:

         Use the IP address to log in to the instance for which the alarm is generated as user **root** and run the **free -g** command to check the value of **Mem** in the **free** column. The value indicates the available memory of the node. In the following example, the available memory of the node is 4 GB.

         .. code-block::

                          total        used        free      shared  buff/cache   available
            Mem:            112          48           4          10          58          46
            ......

         If the value of **Mem** is at least that of **-Xmx**, the node memory is sufficient. If the value of **Mem** is less than that of **-Xmx**, the node memory is insufficient.

      -  If yes, change the value of **-XX:MaxDirectMemorySize** to that of **-Xmx**.
      -  If no, increase **-XX:MaxDirectMemorySize** to a value no larger than that of **Mem**.

   b. Save the configuration and restart the DataNode instances.

#. .. _alm-14016__li111010376180:

   Check whether **ALM-14008 DataNode Heap Memory Usage Exceeds the Threshold** exists.

   -  If yes, rectify the fault by referring to **ALM-14008 DataNode Heap Memory Usage Exceeds the Threshold**.
   -  If no, go to :ref:`7 <alm-14016__li5868287393722>`.

#. .. _alm-14016__li5868287393722:

   Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-14016__li5838381193722>`.

**Collect the fault information.**

8.  .. _alm-14016__li5838381193722:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **DataNode** for the target cluster.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927713.png
