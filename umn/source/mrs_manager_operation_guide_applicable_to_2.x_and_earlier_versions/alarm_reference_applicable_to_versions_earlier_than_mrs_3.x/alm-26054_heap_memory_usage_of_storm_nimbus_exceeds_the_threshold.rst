:original_name: alm_26054.html

.. _alm_26054:

ALM-26054 Heap Memory Usage of Storm Nimbus Exceeds the Threshold
=================================================================

Description
-----------

The system checks the heap memory usage of Storm Nimbus every 30 seconds and compares it with the threshold. This alarm is generated if the heap memory usage exceeds the threshold (80% by default).

To modify the threshold, users can choose **System** > **Threshold Configuration** > **Service** > **Storm** on MRS Manager.

This alarm is cleared if the heap memory usage is lower than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
26054    Major          Yes
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

Frequent memory garbage collection or memory overflow may occur, affecting submission of Storm services.

Possible Causes
---------------

The heap memory usage is high or the heap memory is improperly allocated.

Procedure
---------

#. Check the heap memory usage.

   a. Go to the cluster details page and choose **Alarms**.

   b. Choose **ALM-26054 Heap Memory Usage of Storm Nimbus Exceeds the Threshold > Location**. Query the **HostName** of the alarmed instance.

   c. Choose **Components > Storm > Instances > Nimbus (corresponding to the HostName of the alarmed instance) > Customize > Heap Memory Usage of Nimbus**.

   d. Check whether the heap memory usage of Nimbus has reached the threshold (80%).

      -  If yes, go to :ref:`1.e <alm_26054__en-us_topic_0191813940_li3532012320227>`.
      -  If no, go to :ref:`2 <alm_26054__en-us_topic_0191813940_li572522141314>`.

   e. .. _alm_26054__en-us_topic_0191813940_li3532012320227:

      Adjust the heap memory.

      Choose **Components > Storm > Service Configuration**, and set **Type** to **All**. Choose **Nimbus** > **System**. Increase the value of **-Xmx** in **NIMBUS_GC_OPTS**. Click **Save Configuration**. Select **Restart the affected services or instances** and click **OK**.

   f. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_26054__en-us_topic_0191813940_li572522141314>`.

#. .. _alm_26054__en-us_topic_0191813940_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Related Information
-------------------

N/A
