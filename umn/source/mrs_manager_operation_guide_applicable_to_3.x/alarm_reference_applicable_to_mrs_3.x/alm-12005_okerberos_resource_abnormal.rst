:original_name: ALM-12005.html

.. _ALM-12005:

ALM-12005 OKerberos Resource Abnormal
=====================================

Description
-----------

The alarm module checks the status of the Kerberos resource in Manager every 80 seconds. This alarm is generated when the alarm module detects that the Kerberos resources are abnormal for six consecutive times.

This alarm is cleared when the Kerberos resource recovers and the alarm handling is complete.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12005    Major          Yes
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

The component WebUI authentication services are unavailable and cannot provide security authentication functions for web upper-layer services. Users may be unable to log in to MRS Manager and the WebUIs of components.

Possible Causes
---------------

The OLdap resource on which the Okerberos depends is abnormal.

Procedure
---------

**Check whether the OLdap resource on which the Okerberos depends is abnormal in the Manager.**

#. Log in the Manager node in the cluster as user **omm**.

   Log in to MRS Manager using the floating IP address, and run the **sh ${BIGDATA_HOME}/om-server/om/sbin/status-oms.sh** command to check the information about the current Manager two-node cluster.

#. Run the **sh ${BIGDATA_HOME}/om-server/OMS/workspace0/ha/module/hacom/script/status_ha.sh** command to check whether the OLdap resource status managed by HA is normal. (In single-node mode, the OLdap resource is in the Active_normal state; in the two-node mode, the OLdap resource is in the Active_normal state on the active node and in the Standby_normal state on the standby node.)

   -  If yes, go to :ref:`4 <alm-12005__li34421516164820>`.
   -  If no, go to :ref:`3 <alm-12005__li4031832916486>`.

#. .. _alm-12005__li4031832916486:

   See the procedure in :ref:`ALM-12004 OLdap Resource Abnormal <alm-12004>` to resolve the problem. After the OLdap resource status recovers, check whether the OKerberos resource status is normal.

   -  If yes, the operation is complete.
   -  If no, go to :ref:`4 <alm-12005__li34421516164820>`.

**Collect fault information.**

4. .. _alm-12005__li34421516164820:

   On the MRS Manager home page, choose **O&M** > **Log > Download**.

5. Select **OmsKerberos** and **OmmServer** from the **Service** and click **OK**.

6. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532607838.png
