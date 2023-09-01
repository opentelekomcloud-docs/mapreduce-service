:original_name: ALM-25500.html

.. _ALM-25500:

ALM-25500 KrbServer Service Unavailable
=======================================

Description
-----------

The system checks the KrbServer service status every 30 seconds. This alarm is generated when the system detects that the KrbServer service is abnormal.

This alarm is cleared when the system detects that the KrbServer service is normal.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
25500    Critical       Yes
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

When this alarm is generated, no operation can be performed for the KrbServer component in the cluster. The authentication of KrbServer in other components will be affected. The running status of components that depend on KrbServer in the cluster is Bad.

Possible Causes
---------------

-  The node where the KrbServer service locates is faulty.
-  The OLdap service is abnormal.

Procedure
---------

**Check whether the node where the KrbServer service locates is faulty.**

#. .. _alm-25500__li19872481202241:

   On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **KrbServer** > **Instance** to go to the KrbServer instance page to obtain the host name of the node where the KrbServer service locates.

#. On the **Alarm** page of the FusionInsight Manager system, check whether any alarm of **Node Fault** exists.

   -  If yes, go to :ref:`3 <alm-25500__li6642034202241>`.
   -  If no, go to :ref:`6 <alm-25500__li25144643202241>`.

#. .. _alm-25500__li6642034202241:

   Check whether the host name in the alarm is consistent with the :ref:`1 <alm-25500__li19872481202241>` host name.

   -  If yes, go to :ref:`4 <alm-25500__li1133847202241>`.
   -  If no, go to :ref:`6 <alm-25500__li25144643202241>`.

#. .. _alm-25500__li1133847202241:

   Handle the alarm according to "ALM-12006 Node Fault".

#. Check whether **KrbServer Service Unavailable** is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-25500__li25144643202241>`.

**Check whether the OLdap service is normal.**

6. .. _alm-25500__li25144643202241:

   On the **Alarm** page of the FusionInsight Manager system, check whether any alarm of **OLdap Resource Abnormal** exists.

   -  If yes, go to :ref:`7 <alm-25500__li23450230202241>`.
   -  If no, go to :ref:`9 <alm-25500__li11814745202241>`.

7. .. _alm-25500__li23450230202241:

   Handle the alarm according to "ALM-12004 OLdap Resource Abnormal".

8. Check whether **KrbServer Service Unavailable** is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-25500__li11814745202241>`.

**Collect fault information.**

9.  .. _alm-25500__li11814745202241:

    On the FusionInsight Manager, choose **O&M** > **Log > Download**.

10. Select **KrbServer** in the required cluster from the **Service**.

11. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448298.png
