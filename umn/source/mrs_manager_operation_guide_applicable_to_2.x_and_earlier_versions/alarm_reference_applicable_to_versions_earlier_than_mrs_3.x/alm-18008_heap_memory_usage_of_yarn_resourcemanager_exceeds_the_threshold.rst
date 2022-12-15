:original_name: alm_18008.html

.. _alm_18008:

ALM-18008 Heap Memory Usage of Yarn ResourceManager Exceeds the Threshold
=========================================================================

Description
-----------

The system checks the heap memory usage of Yarn ResourceManager every 30 seconds and compares the actual usage with the threshold. The alarm is generated when the heap memory usage of Yarn ResourceManager exceeds the threshold (80% of the maximum memory by default).

To change the threshold, choose **System** > **Threshold Configuration** > **Service** > **Yarn**. The alarm is cleared when the heap memory usage is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
18008    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+---------------------------------------------------------+
| Parameter         | Description                                             |
+===================+=========================================================+
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

When the heap memory usage of Yarn ResourceManager is overhigh, the performance of Yarn task submission and operation is affected. What is more, a memory overflow occurs so that the Yarn service is unavailable.

Possible Causes
---------------

The heap memory of the Yarn ResourceManager instance on the node is overused or the heap memory is inappropriately allocated. As a result, the usage exceeds the threshold.

Procedure
---------

#. Check the heap memory usage.

   a. Go to the MRS cluster details page and choose **Alarms**.

   b. Select the alarm whose **Alarm ID** is **18008** and view the IP address and role name of the instance in **Location**.

   c. Choose **Components** > **Yarn** > **Instances** > **ResourceManager** (IP address of the instance for which the alarm is generated) > **Customize** > **Percentage of Used Heap Memory of the ResourceManager**. Check the heap memory usage.

   d. Check whether the heap memory usage of ResourceManager has reached the threshold (80% of the maximum memory).

      -  If yes, go to :ref:`1.e <alm_18008__en-us_topic_0191813919_li1011493181634>`.
      -  If no, go to :ref:`2 <alm_18008__en-us_topic_0191813919_li572522141314>`.

   e. .. _alm_18008__en-us_topic_0191813919_li1011493181634:

      Choose **Components** > **Yarn** > **Service Configuration**. Set **Type** to **All** and choose **ResourceManager** > **System**. Change the values of **-Xmx** and **-Xms** in the **GC_OPTS** parameter based on the site requirements to ensure that the value of **-Xms** is less than that of **-Xmx**. Click **Save Configuration** and select **Restart Role Instance**. Click **OK**.

   f. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_18008__en-us_topic_0191813919_li572522141314>`.

#. .. _alm_18008__en-us_topic_0191813919_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
