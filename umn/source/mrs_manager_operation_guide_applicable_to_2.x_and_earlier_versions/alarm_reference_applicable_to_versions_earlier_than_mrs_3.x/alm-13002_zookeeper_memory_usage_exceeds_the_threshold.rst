:original_name: alm_13002.html

.. _alm_13002:

ALM-13002 ZooKeeper Memory Usage Exceeds the Threshold
======================================================

Description
-----------

The system checks the ZooKeeper service status every 30 seconds. The alarm is generated when the memory usage of a ZooKeeper instance exceeds the threshold (80% of the maximum memory).

The alarm is cleared when the memory usage is less than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
13002    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+-------------------------------------------------------------------------------------+
| Parameter         | Description                                                                         |
+===================+=====================================================================================+
| ServiceName       | Specifies the service for which the alarm is generated.                             |
+-------------------+-------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                |
+-------------------+-------------------------------------------------------------------------------------+
| Trigger Condition | Generates an alarm when the actual indicator value exceeds the specified threshold. |
+-------------------+-------------------------------------------------------------------------------------+

Impact on the System
--------------------

If the available ZooKeeper memory is insufficient, a memory overflow occurs and the service breaks down.

Possible Causes
---------------

The memory usage of the ZooKeeper instance is overused or the memory is inappropriately allocated.

Procedure
---------

#. Check the memory usage.

   a. On the MRS cluster details page, choose **Alarms** > **ALM-13002 ZooKeeper Memory Usage Exceeds the Threshold** > **Location**. Check the IP address of the instance for which the alarm is generated.

   b. On the MRS cluster details page, choose **Components** > **ZooKeeper** > **Instances** > **quorumpeer** (IP address of the instance for which the alarm is generated) > **Customize** > **ZooKeeper Heap And Direct Buffer Resource**. Check the heap memory usage.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and choose **Services** > **ZooKeeper** > **Instance** > **quorumpeer** (IP address of the instance for which the alarm is generated) > **Customize** > **ZooKeeper Heap And Direct Buffer Resource**. Check the heap memory usage.

   c. Check whether the used heap memory of ZooKeeper reaches 80% of the maximum heap memory specified for ZooKeeper.

      -  If yes, go to :ref:`1.d <alm_13002__en-us_topic_0191813895_cn_58_42_000001_3_mmccppss_stepb2>`.
      -  If no, go to :ref:`1.f <alm_13002__en-us_topic_0191813895_cn_58_42_000001_3_mmccppss_stepb4>`.

   d. .. _alm_13002__en-us_topic_0191813895_cn_58_42_000001_3_mmccppss_stepb2:

      On MRS Manager, choose **Services** > **ZooKeeper** > **Configuration** > **All** > **quorumpeer** > **System**. Increase the value of **-Xmx** in **GC_OPTS** as required.

   e. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`1.f <alm_13002__en-us_topic_0191813895_cn_58_42_000001_3_mmccppss_stepb4>`.

   f. .. _alm_13002__en-us_topic_0191813895_cn_58_42_000001_3_mmccppss_stepb4:

      On the MRS cluster details page, choose **Components** > **ZooKeeper** > **Instances** > **quorumpeer** (IP address of the instance for which the alarm is generated) > **Customize** > **ZooKeeper Heap And Direct Buffer Resource**. Check the direct buffer memory usage.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and choose **Services** > **ZooKeeper** > **Instance** > **quorumpeer** (IP address of the instance for which the alarm is generated) > **Customize** > **ZooKeeper Heap And Direct Buffer Resource**. Check the direct buffer memory usage.

   g. Check whether the used direct buffer memory of ZooKeeper reaches 80% of the maximum direct buffer memory specified for ZooKeeper.

      -  If yes, go to :ref:`1.h <alm_13002__en-us_topic_0191813895_li49457583153150>`.
      -  If no, go to :ref:`2 <alm_13002__en-us_topic_0191813895_li572522141314>`.

   h. .. _alm_13002__en-us_topic_0191813895_li49457583153150:

      On the MRS cluster details page, choose **Components** > **ZooKeeper** > **Service Configuration**. Set **Type** to **All** and choose **quorumpeer** > **System**.

      Increase the value of **-XX:MaxDirectMemorySize** in **GC_OPTS** as required.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager, choose **Services** > **ZooKeeper** > **Service Configuration**. Set **Type** to **All** and choose **quorumpeer** > **System**.

   i. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_13002__en-us_topic_0191813895_li572522141314>`.

#. .. _alm_13002__en-us_topic_0191813895_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
