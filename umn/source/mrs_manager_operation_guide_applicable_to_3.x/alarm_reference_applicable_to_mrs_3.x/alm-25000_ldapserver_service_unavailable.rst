:original_name: ALM-25000.html

.. _ALM-25000:

ALM-25000 LdapServer Service Unavailable
========================================

Description
-----------

The system checks the LdapServer service status every 30 seconds. This alarm is generated when the system detects that both the active and standby LdapServer services are abnormal.

This alarm is cleared when the system detects that one or two LdapServer services are normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
25000    Critical       Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

When this alarm is generated, no operation can be performed for the KrbServer users and LdapServer users in the cluster. For example, users, user groups, or roles cannot be added, deleted, or modified, and user passwords cannot be changed on the MRS Manager portal. The authentication for existing users in the cluster is not affected.

Possible Causes
---------------

-  The node where the LdapServer service locates is faulty.
-  The LdapServer process is abnormal.

Procedure
---------

**Check whether the nodes where the two SlapdServer instances of the LdapServer service are located are faulty.**

#. .. _alm-25000__li1018355492146:

   On MRS Manager, choose **Cluster >** *Name of the desired cluster* **> Services** > **LdapServer** > **Instance** to go to the LdapServer instance page to obtain the host name of the node where the two SlapdServer instances locates.

#. Choose **O&M > Alarm > Alarms**. On the **Alarm** page of the MRS Manager system, check whether any alarm of **Node Fault** exists.

   -  If yes, go to :ref:`3 <alm-25000__li3636395592146>`.
   -  If no, go to :ref:`6 <alm-25000__li6664070892146>`.

#. .. _alm-25000__li3636395592146:

   Check whether the host name in the alarm is consistent with the :ref:`1 <alm-25000__li1018355492146>` host name.

   -  If yes, go to :ref:`4 <alm-25000__li5979927992146>`.
   -  If no, go to :ref:`6 <alm-25000__li6664070892146>`.

#. .. _alm-25000__li5979927992146:

   Handle the alarm according to "ALM-12006 Node Fault".

#. Check whether **LdapServer Service Unavailable** is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-25000__li4495032292146>`.

**Check whether the LdapServer process is normal.**

6. .. _alm-25000__li6664070892146:

   Choose **O&M > Alarm > Alarms**. On the **Alarm** page of the MRS Manager system, check whether any alarm of **Process Fault** exists.

   -  If yes, go to :ref:`7 <alm-25000__li4274962392146>`.
   -  If no, go to :ref:`10 <alm-25000__li4495032292146>`.

7. .. _alm-25000__li4274962392146:

   Check whether the service and host name in the alarm are consistent with the LdapServer service and host name.

   -  If yes, go to :ref:`8 <alm-25000__li4016743392146>`.
   -  If no, go to :ref:`10 <alm-25000__li4495032292146>`.

8. .. _alm-25000__li4016743392146:

   Handle the alarm according to "ALM-12007 Process Fault".

9. Check whether **LdapServer Service Unavailable** is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-25000__li4495032292146>`.

**Collect fault information.**

10. .. _alm-25000__li4495032292146:

    On the MRS Manager, choose **O&M** > **Log > Download**.

11. Select **LdapServer** in the required cluster from the **Service**.

12. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

13. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448278.png
