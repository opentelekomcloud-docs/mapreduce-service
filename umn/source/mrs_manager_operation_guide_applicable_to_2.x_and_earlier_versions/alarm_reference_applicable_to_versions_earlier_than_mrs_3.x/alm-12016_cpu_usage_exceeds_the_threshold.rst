:original_name: alm_12016.html

.. _alm_12016:

ALM-12016 CPU Usage Exceeds the Threshold
=========================================

Description
-----------

The system checks the CPU usage every 30 seconds and compares the check result with the default threshold. The CPU usage has a default threshold. This alarm is generated when the CPU usage exceeds the threshold for several times (configurable, 10 times by default) consecutively.

This alarm is cleared when the average CPU usage is less than or equal to 90% of the threshold.

**Attribute**
-------------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12016    Major          Yes
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

Processes respond slowly or do not work.

Possible Causes
---------------

-  The alarm threshold or alarm hit number is improperly configured.
-  The CPU configuration cannot meet service requirements. The CPU usage reaches the upper limit.

Procedure
---------

#. Check whether the alarm threshold or alarm hit number is properly configured.

   a. Log in to MRS Manager and change the alarm threshold and alarm hit number based on CPU usage.
   b. Choose **System** > **Threshold Configuration** > **Device** > **Host** > **CPU** > **CPU Usage** > **CPU Usage** and change the alarm threshold based on the actual CPU usage.
   c. Choose **System** > **Threshold Configuration** > **Device** > **Host** > **CPU** > **CPU Usage** > **CPU Usage** and change **hit number** based on the actual CPU usage.

      .. note::

         This option defines the alarm check phase. **Interval** indicates the alarm check period and **hit number** indicates the number of times when the CPU usage exceeds the threshold. An alarm is generated when the CPU usage exceeds the threshold for several times consecutively.

   d. Wait 2 minutes and check whether the alarm is automatically cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12016__en-us_topic_0191813922_li23374914104744>`.

#. .. _alm_12016__en-us_topic_0191813922_li23374914104744:

   Expand the system.

   a. Go to the MRS cluster details page. In the alarm list on the alarm management tab page, click the row that contains the alarm. In the alarm details, view the address of the node.
   b. Log in to the node for which the alarm is generated.
   c. Run **cat /proc/stat \| awk 'NR==1'|awk '{for(i=2;i<=NF;i++)j+=$i;print "" 100 - ($5+$6) \* 100 / j;}'** to check the system CPU usage.
   d. If the CPU usage exceeds the threshold, expand the CPU capacity.
   e. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_12016__en-us_topic_0191813922_li572522141314>`.

#. .. _alm_12016__en-us_topic_0191813922_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

**Reference**
-------------

None
