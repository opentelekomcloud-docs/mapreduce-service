:original_name: alm_12053.html

.. _alm_12053:

ALM-12053 File Handle Usage Exceeds the Threshold
=================================================

Description
-----------

The system checks the handler usage every 30 seconds. This alarm is generated when the handle usage exceeds the threshold (the default threshold is **80%**) for multiple times (the default value is **5**).

You can change the threshold by choosing **System** > **Threshold Configuration** > **Device** > **Host** > **Host Status** > **Host File Handle Usage** > **Host File Handle Usage**.

If the **hit number** is **1**, this alarm is cleared when the file handle usage is less than or equal to the threshold. If the **hit number** is greater than **1**, this alarm is cleared when the file handle usage is less than or equal to 90% of the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12053    Major          Yes
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

The system applications fail to open files, access networks, and perform other I/O operations. The applications are running improperly.

Possible Causes
---------------

-  The number of file handles does not meet service requirements.
-  The system is abnormal.

Procedure
---------

**Increase the number of file handles.**

#. Go to the MRS cluster details page and choose **Alarms**.
#. In the real-time alarm list, click the alarm. In the **Alarm Details** area, obtain the IP address of the host for which the alarm is generated.
#. Use PuTTY to log in to the host for which the alarm is generated as user **root**.
#. Run the **ulimit -n** command to check the maximum number of handles set in the system.
#. If the file handle usage exceeds the threshold, contact the system administrator to increase the number of system file handles.
#. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm_12053__en-us_topic_0191813957_en-us_topic_0087039427_li6831599151742>`.

**Check whether the system environment is normal.**

7. .. _alm_12053__en-us_topic_0191813957_en-us_topic_0087039427_li6831599151742:

   Contact the system administrator to check whether the OS is abnormal.

   -  If yes, rectify the operating system fault and go to :ref:`8 <alm_12053__en-us_topic_0191813957_en-us_topic_0087039427_li2777630151742>`.
   -  If no, go to :ref:`9 <alm_12053__en-us_topic_0191813957_li572522141314>`.

8. .. _alm_12053__en-us_topic_0191813957_en-us_topic_0087039427_li2777630151742:

   Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm_12053__en-us_topic_0191813957_li572522141314>`.

9. .. _alm_12053__en-us_topic_0191813957_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
