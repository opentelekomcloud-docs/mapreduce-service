:original_name: alm_18004.html

.. _alm_18004:

ALM-18004 NodeManager Disk Usability Ratio Is Lower Than the Threshold
======================================================================

Description
-----------

The system checks the available disk space of each NodeManager node every 30 seconds and compares the disk availability rate with the threshold. A default threshold range is provided for the **NodeManager Disk Usability Ratio**. This alarm is generated when the system detects that the actual **NodeManager Disk Usability Ratio** is lower than the threshold.

This alarm is automatically cleared when the value of **NodeManager Disk Usability Ratio** is greater than the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
18004    Major          Yes
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
| Trigger condition | Specifies the threshold for triggering the alarm.       |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

-  The NodeManager node whose disk availability rate is lower than the threshold may fail to provide the Yarn service.
-  The number of containers decreases, so the cluster performance may deteriorate.

Possible Causes
---------------

-  The disk space of the host where the NodeManager node resides is insufficient.
-  User **omm** does not have the permission to access a local directory on the NodeManager node.

Procedure
---------

#. Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
