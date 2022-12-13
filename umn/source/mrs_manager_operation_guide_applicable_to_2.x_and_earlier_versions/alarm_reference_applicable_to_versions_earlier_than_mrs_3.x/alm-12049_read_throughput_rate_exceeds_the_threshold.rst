:original_name: alm_12049.html

.. _alm_12049:

ALM-12049 Read Throughput Rate Exceeds the Threshold
====================================================

Description
-----------

The system checks the read throughput rate every 30 seconds. This alarm is generated when the read throughput rate exceeds the threshold (the default threshold is **80%**) for multiple times (the default value is **5**).

You can change the threshold by choosing **System** > **Threshold Configuration** > **Device** > **Host** > **Network Reading** > **Network Read Throughput Rate** > **Read Throughput Rate**.

If the **hit number** is **1**, this alarm is cleared when the read throughput rate is less than or equal to the threshold. If the **hit number** is greater than **1**, this alarm is cleared when the read throughput rate is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12049    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+--------------------------------------------------------------+
| Parameter         | Description                                                  |
+===================+==============================================================+
| ServiceName       | Specifies the service for which the alarm is generated.      |
+-------------------+--------------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.         |
+-------------------+--------------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.         |
+-------------------+--------------------------------------------------------------+
| NetworkCardName   | Specifies the network port for which the alarm is generated. |
+-------------------+--------------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.            |
+-------------------+--------------------------------------------------------------+

Impact on the System
--------------------

The service system runs abnormally or is unavailable.

Possible Causes
---------------

-  The alarm threshold is improperly configured.
-  The network port rate does not meet service requirements.

Procedure
---------

**Check whether the threshold is set properly.**

#. Log in to MRS Manager and check whether the threshold (configurable, 80% by default) is appropriate.

   -  If yes, go to :ref:`2 <alm_12049__en-us_topic_0191813925_en-us_topic_0087039310_li5311586145835>`.
   -  If no, go to :ref:`4 <alm_12049__en-us_topic_0191813925_en-us_topic_0087039310_li17726490145835>`.

#. .. _alm_12049__en-us_topic_0191813925_en-us_topic_0087039310_li5311586145835:

   Choose **System** > **Threshold Configuration** > **Device** > **Host** > **Network Reading** > **Network Read Throughput Rate** > **Read Throughput Rate** to change the alarm threshold based on the actual service usage.

#. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm_12049__en-us_topic_0191813925_en-us_topic_0087039310_li17726490145835>`.

**Check whether the network port rate meets the requirements.**

4. .. _alm_12049__en-us_topic_0191813925_en-us_topic_0087039310_li17726490145835:

   In the real-time alarm list, click the alarm. In the **Alarm Details** area, obtain the IP address and network port name of the host for which the alarm is generated.

5. Use PuTTY to log in to the host for which the alarm is generated as user **root**.

6. Run the **ethtool** *network port name* command to check the maximum network port rate **Speed**.

   .. note::

      In a VM environment, you may fail to obtain the network port rate by running commands. You are advised to contact the system administrator to check whether the network port rate meets the requirements.

7. If the read throughput rate exceeds the threshold, contact the system administrator to increase the network port rate.

8. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm_12049__en-us_topic_0191813925_li572522141314>`.

9. .. _alm_12049__en-us_topic_0191813925_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
