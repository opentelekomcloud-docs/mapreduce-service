:original_name: ALM-12172.html

.. _ALM-12172:

ALM-12172 Failed to Report Metrics to Cloud Eye
===============================================

Description
-----------

After metric sharing is enabled for a cluster, the Controller periodically collects cluster metrics and reports them to Cloud Eye.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12172    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

MRS monitoring metrics are unavailable on Cloud Eye.

Possible Causes
---------------

-  Failed to call Cloud Eye APIs due to insufficient permissions.
-  Failed to report data to Cloud Eye due to network problems.
-  Failed to report data to Cloud Eye due to internal errors.

Procedure
---------

#. On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. On the page that is displayed, click |image1| in the row containing the alarm and view the additional information of the alarm.
#. Rectify the fault based on the following scenarios:

   -  If "Call CES to send metrics fail. Permission exception" is displayed in the additional information, the token of the resource tenant is invalid. Restart the Controller and obtain the token again.
   -  If "Call CES to send metrics fail. Request CES error code xxx" is displayed in the additional information, an error occurs in the request to Cloud Eye. Check the network connectivity and authentication information.
   -  If "Call CES to send metrics fail. CES internal error code xxx" is displayed in the additional information, the Cloud Eye service encounters an internal error and is unavailable. Contact O&M personnel and send collected fault logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607954.png
