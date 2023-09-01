:original_name: ALM-12072.html

.. _ALM-12072:

ALM-12072 FloatIP Resource Is Abnormal
======================================

Description
-----------

HA checks the floatip resources of Manager every 9 seconds. This alarm is generated when HA detects that the floatip resources are abnormal for 3 consecutive times.

This alarm is cleared when the FloatIP resource is normal.

**Resource Type** of FloatIP is **Single-active**. Active/standby will be triggered upon resource exceptions. When this alarm is generated, the active/standby switchover is complete and new FloatIP resources have been enabled on the new active FusionInsight Manager. In this case, this alarm is cleared. This alarm is used to notify users of the cause of the active/standby switchover.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12072    Major          Yes
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

-  The active/standby FusionInsight Manager switchover occurs.
-  The FloatIP process is repeatedly restarts, which may lead to the failure to visit the native service UI.

Possible Causes
---------------

-  The floating IP address is abnormal.

Procedure
---------

**Check the floating IP address status of the active management node.**

#. In the alarm list on FusionInsight Manager, locate the row that contains the alarm, and view the address of the host for which the alarm is generated and the resource name.

#. Log in to the active management node as user **root**.

#. Run the following command, go to the **${BIGDATA_HOME}/om-server/om/sbin/** directory.

   **su - omm**

   **cd** **${BIGDATA_HOME}/om-server/om/sbin/**

#. Run the **sh status-oms.sh** command, and execute the **status-oms.sh** script to check whether the floating IP address of the active FusionInsight Manager is normal. View the command output, locate the row where **ResName** is **floatip**, and check whether the following information is displayed.

   For example:

   .. code-block::

      10-10-10-160 floatip Normal Normal Single_active

   -  If it is, go to :ref:`8 <alm-12072__li726861151715>`.
   -  If it is not, go to :ref:`5 <alm-12072__li162681212172>`.

#. .. _alm-12072__li162681212172:

   Run the **ifconfig** command to check whether the NIC with the floating IP address exists.

   -  If it does, go to :ref:`8 <alm-12072__li726861151715>`.
   -  If it does not, go to :ref:`6 <alm-12072__li19269111111714>`.

#. .. _alm-12072__li19269111111714:

   Run the **ifconfig** *NIC name Floating IPaddress* netmask *Subnet mask* command to reconfigure the NIC with the floating IP address. (For example, **ifconfig eth0 10.10.10.102 netmask 255.255.255.0**).

#. Five minutes later, check whether the alarm is cleared.

   -  If it is, no further action is required.
   -  If it is not, go to :ref:`8 <alm-12072__li726861151715>`.

**Collect fault information.**

8.  .. _alm-12072__li726861151715:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

9.  Select **Controller** and **OmmServer** for **Service** and click **OK**.

10. Click |image1| in the upper right corner. In the displayed dialog box, set **Start Date** and **End Date** to 1 hour before and after the alarm generation time respectively and click **OK**. Then, click **Download**.

11. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

This alarm will be automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807857.png
