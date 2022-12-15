:original_name: alm_12046.html

.. _alm_12046:

ALM-12046 Write Packet Dropped Rate Exceeds the Threshold
=========================================================

Description
-----------

The system checks the write packet dropped rate every 30 seconds. This alarm is generated when the write packet dropped rate exceeds the threshold (the default threshold is 0.5%) for multiple times (the default value is **5**).

You can change the threshold by choosing **System** > **Threshold Configuration** > **Device** > **Host** > **Network Writing** > **Network Write Packet Rate Information** > **Write Packet Dropped Rate**.

When the **hit number** is **1**, this alarm is cleared when the network write packet dropped rate is less than or equal to the threshold. When the **hit number** is greater than **1**, this alarm is cleared when the network write packet dropped rate is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12046    Major          Yes
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

The service performance deteriorates or some services time out.

Possible Causes
---------------

-  The alarm threshold is improperly configured.
-  The network environment is abnormal.

Procedure
---------

**Check whether the threshold is set properly.**

#. Log in to MRS Manager and check whether the threshold (configurable, 0.5% by default) is appropriate.

   -  If yes, go to :ref:`4 <alm_12046__en-us_topic_0191813915_en-us_topic_0087039332_li4369794811450>`.
   -  If no, go to :ref:`2 <alm_12046__en-us_topic_0191813915_en-us_topic_0087039332_li5699560811450>`.

#. .. _alm_12046__en-us_topic_0191813915_en-us_topic_0087039332_li5699560811450:

   Choose **System** > **Threshold Configuration** > **Device** > **Host** > **Network Write Information** > **Network Write Packet Rate** > **Write Packet Dropped Rate** and change the alarm threshold based on the actual service usage.

#. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm_12046__en-us_topic_0191813915_en-us_topic_0087039332_li4369794811450>`.

**Check whether the network is normal.**

4. .. _alm_12046__en-us_topic_0191813915_en-us_topic_0087039332_li4369794811450:

   Contact the system administrator to check whether the network is normal.

   -  If yes, rectify the network fault and go to :ref:`5 <alm_12046__en-us_topic_0191813915_en-us_topic_0087039332_li6056359711450>`.
   -  If no, go to :ref:`6 <alm_12046__en-us_topic_0191813915_li572522141314>`.

5. .. _alm_12046__en-us_topic_0191813915_en-us_topic_0087039332_li6056359711450:

   Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm_12046__en-us_topic_0191813915_li572522141314>`.

6. .. _alm_12046__en-us_topic_0191813915_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
