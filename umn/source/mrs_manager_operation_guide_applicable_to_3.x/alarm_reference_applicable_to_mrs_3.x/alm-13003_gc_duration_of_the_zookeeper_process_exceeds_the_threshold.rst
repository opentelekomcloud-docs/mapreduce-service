:original_name: ALM-13003.html

.. _ALM-13003:

ALM-13003 GC Duration of the ZooKeeper Process Exceeds the Threshold
====================================================================

Description
-----------

The system checks the garbage collection (GC) duration of the ZooKeeper process every 60 seconds. This alarm is generated when the GC duration exceeds the threshold (12 seconds by default).

This alarm is cleared when the GC duration is less than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
13003    Major          Yes
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

A long GC duration of the ZooKeeper process may interrupt the services.

Possible Causes
---------------

The heap memory of the ZooKeeper process is overused or inappropriately allocated, causing frequent occurrence of the GC process.

Procedure
---------

**Check the GC duration.**

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. On the displayed page, click the drop-down list of **GC Duration of the ZooKeeper Process Exceeds the Threshold**. View the IP address of the instance for which the alarm is generated.

#. On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **ZooKeeper** > **Instance** > **quorumpeer**. Click the drop-down list in the upper right corner of **Chart**, choose **Customize** > **GC**, select **ZooKeeper GC Duration per Minute**, and click **OK** to check the GC duration statistics of the ZooKeeper process collected every minute.

#. Check whether the GC duration of the ZooKeeper process collected every minute exceeds the threshold (12 seconds by default).

   -  If yes, go to :ref:`4 <alm-13003__li1332215316392>`.
   -  If no, go to :ref:`8 <alm-13003__li12535847161327>`.

#. .. _alm-13003__li1332215316392:

   Check whether memory leakage occurs in the application.

#. On the **Home** page of MRS Manager, choose **Cluster** > **Services** > **ZooKeeper**. On the page that is displayed, click the **Configuration** tab then the **All Configurations** sub-tab, and select **quorumpeer** > **System**. Increase the value of the **GC_OPTS** parameter as required.

   .. note::

      Generally, **-Xmx** is twice of ZooKeeper data capacity. If the capacity of ZooKeeper reaches 2 GB, set **GC_OPTS** as follows:

      -Xms4G -Xmx4G -XX:NewSize=512M -XX:MaxNewSize=512M -XX:MetaspaceSize=64M -XX:MaxMetaspaceSize=64M -XX:CMSFullGCsBeforeCompaction=1

#. Save the configuration and restart the ZooKeeper service.

#. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-13003__li12535847161327>`.

**Collect the fault information.**

8.  .. _alm-13003__li12535847161327:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **ZooKeeper** for the target cluster.

10. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

11. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927350.png
