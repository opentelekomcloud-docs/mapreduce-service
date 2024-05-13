:original_name: ALM-12049.html

.. _ALM-12049:

ALM-12049 Network Read Throughput Rate Exceeds the Threshold
============================================================

Description
-----------

The system checks the network read throughput rate every 30 seconds and compares the actual throughput rate with the threshold (the default threshold is 80%). This alarm is generated when the system detects that the network read throughput rate exceeds the threshold for several times (5 times by default) consecutively.

To change the threshold, choose **O&M > Alarm** > **Thresholds** > *Name of the desired cluster* > **Host** > **Network Reading** > **Read Throughput Rate**.

When the **Trigger Count** is 1, this alarm is cleared when the network read throughput rate is less than or equal to the threshold. When the **Trigger Count** is greater than 1, this alarm is cleared when the network read throughput rate is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12049    Major          Yes
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
| NetworkCardName   | Specifies the network port for which the alarm is generated.                                                                 |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+
| Trigger Condition | Specifies the threshold triggering the alarm. If the current indicator value exceeds this threshold, the alarm is generated. |
+-------------------+------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

The service system runs improperly or is unavailable.

Possible Causes
---------------

-  The alarm threshold is set improperly.
-  The network port rate cannot meet the current service requirements.

Procedure
---------

**Check whether the threshold is set properly.**

#. On the MRS Manager, choose **O&M > Alarm** > **Thresholds** > *Name of the desired cluster* > **Host** > **Network Reading** > **Read Throughput Rate** and check whether the alarm threshold is set properly. (By default, 80% is a proper value. However, users can configure the value as required.)

   -  If yes, go to :ref:`2 <alm-12049__li5611086815131>`.
   -  If no, go to :ref:`4 <alm-12049__li3065917315131>`.

#. .. _alm-12049__li5611086815131:

   Based on actual usage condition, choose **O&M > Alarm** > **Thresholds** > *Name of the desired cluster* > **Host** > **Network Reading** > **Read Throughput Rate** and click **Modify** in the **Operation** column to modify the alarm threshold.

   For details, see :ref:`Figure 1 <alm-12049__fig566375315131>`.

   .. _alm-12049__fig566375315131:

   .. figure:: /_static/images/en-us_image_0000001532448486.png
      :alt: **Figure 1** Setting alarm thresholds

      **Figure 1** Setting alarm thresholds

#. Wait for 5 minutes, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-12049__li3065917315131>`.

**Check whether the network port rate can meet the service requirements.**

4. .. _alm-12049__li3065917315131:

   On MRS Manager, click |image1| in the row where the alarm is located in the real-time alarm list and obtain the IP address of the host and the network port name for which the alarm is generated.

5. Log in to the host for which the alarm is generated as user **root**.

6. Run the **ethtool** *network port name* command to check the maximum speed of the current network port.

   .. note::

      In the VM environment, you cannot run a command to query the network port rate. It is recommended that you contact the system administrator to confirm whether the network port rate meets the requirements.

7. If the network read throughput rate exceeds the threshold, contact the system administrator to increase the network port rate.

8. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-12049__li4699944215131>`.

**Collect fault information.**

9.  .. _alm-12049__li4699944215131:

    On the MRS Manager home page of the active cluster, choose **O&M** > **Log > Download**.

10. Select **OMS** from the **Service** and click **OK**.

11. Set **Host** to the node for which the alarm is generated and the active OMS node.

12. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582927869.png
.. |image2| image:: /_static/images/en-us_image_0000001582807921.png
