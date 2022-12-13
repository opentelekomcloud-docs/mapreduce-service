:original_name: ALM-12016.html

.. _ALM-12016:

ALM-12016 CPU Usage Exceeds the Threshold
=========================================

Description
-----------

The system checks the CPU usage every 30 seconds and compares the actual CPU usage with the threshold. The CPU usage has a default threshold. This alarm is generated when the CPU usage exceeds the threshold for several times (configurable, 10 times by default) consecutively.

The alarm is cleared in the following two scenarios: The value of **Trigger Count** is 1 and the CPU usage is smaller than or equal to the threshold; the value of **Trigger Count** is greater than 1 and the CPU usage is smaller than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12016    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Name              | Meaning                                                                                                                      |
+===================+==============================================================================================================================+
| Source            | Specifies the cluster or system for which the alarm is generated.                                                            |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated.                                                                      |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.                                                                         |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

Service processes respond slowly or become unavailable.

Possible Causes
---------------

-  The alarm threshold or alarm smoothing times are incorrect.
-  CPU configuration cannot meet service requirements. The CPU usage reaches the upper limit.

Procedure
---------

**Check whether the alarm threshold or alarm Trigger Count are correct.**

#. Change the alarm threshold and alarm **Trigger Count** based on CPU usage.

   On FusionInsight Manager, choose **O&M** > **Alarm** > **Thresholds >** *Name of the desired cluster* > **Host** > **CPU** > **Host CPU Usage** and change the alarm smoothing times based on CPU usage, as shown in :ref:`Figure 1 <alm-12016__fig42676420173938>`.

   .. note::

      This option defines the alarm check phase. **Trigger Count** indicates the alarm check threshold. An alarm is generated when the number of check times exceeds the threshold.

   .. _alm-12016__fig42676420173938:

   .. figure:: /_static/images/en-us_image_0269383824.png
      :alt: **Figure 1** Setting alarm smoothing times

      **Figure 1** Setting alarm smoothing times

   On **Host CPU Usage** page and click **Modify** in the **Operation** column to change the alarm threshold, as shown in :ref:`Figure 2 <alm-12016__fig30961038173938>`.

   .. _alm-12016__fig30961038173938:

   .. figure:: /_static/images/en-us_image_0000001440977805.png
      :alt: **Figure 2** Setting an alarm threshold

      **Figure 2** Setting an alarm threshold

#. After 2 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-12016__li65266749173938>`.

**Check whether the CPU usage reaches the upper limit.**

3. .. _alm-12016__li65266749173938:

   In the alarm list on FusionInsight Manager, click |image1| in the row where the alarm is located to view the alarm host address in the alarm details.

4. On the **Hosts** page, click the node on which the alarm is reported.

5. View the CPU usage for 5 minutes. If the CPU usage exceeds the threshold for multiple times, contact the system administrator to add more CPUs.

6. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-12016__li35735451173938>`.

**Collect fault information.**

7.  .. _alm-12016__li35735451173938:

    On the FusionInsight Manager in the active cluster, choose **O&M** > **Log > Download**.

8.  Select **OmmServer** from the **Service** and click **OK**.

9.  Set **Start Date** for log collection to 10 minutes ahead of the alarm generation time and **End Date** to 10 minutes behind the alarm generation time in **Time Range** and click **Download**.

10. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383826.png
