:original_name: alm_12007.html

.. _alm_12007:

ALM-12007 Process Fault
=======================

Description
-----------

The process health check module checks the process status every 5 seconds. This alarm is generated when the process health check module detects that the process connection status is Bad for three consecutive times.

This alarm is cleared when the process can be connected.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12007    Major          Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The service provided by the process is unavailable.

Possible Causes
---------------

-  The instance process is abnormal.
-  The drive space is insufficient.

Procedure
---------

#. Check whether the instance process is abnormal.

   a. Go to the MRS cluster details page. In the alarm list on the alarm management tab page, click the row that contains the alarm. In the alarm details, view the host name and service name of the alarm.

   b. On the **Alarms** page, check whether the alarm :ref:`ALM-12006 Node Fault <alm_12006>` is generated.

      If yes, go to :ref:`1.c <alm_12007__en-us_topic_0191813896_li2911734163437>`.

      If no, go to :ref:`1.d <alm_12007__en-us_topic_0191813896_li13866005163437>`.

   c. .. _alm_12007__en-us_topic_0191813896_li2911734163437:

      Handle the alarm by following the instructions in :ref:`ALM-12006 Node Fault <alm_12006>`.

   d. .. _alm_12007__en-us_topic_0191813896_li13866005163437:

      Check whether the installation directory user, user group, and permission of the alarm role are correct. The correct user, user group, and the permission are **omm**, **ficommon**, and **750**, respectively.

      -  If yes, go to :ref:`1.f <alm_12007__en-us_topic_0191813896_li46518721164818>`.
      -  If no, go to :ref:`1.e <alm_12007__en-us_topic_0191813896_li56651933164749>`.

   e. .. _alm_12007__en-us_topic_0191813896_li56651933164749:

      Run the following commands to set the permission to **750** and **User:Group** to **omm:ficommon**:

      **chmod 750** *<folder_name>*

      **chown omm:ficommon** *<folder_name>*

   f. .. _alm_12007__en-us_topic_0191813896_li46518721164818:

      Wait 5 minutes and check whether the ALM-12007 Process Fault alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_12007__en-us_topic_0191813896_li1779806016495>`.

#. Check whether the disk space is insufficient.

   a. .. _alm_12007__en-us_topic_0191813896_li1779806016495:

      On the MRS cluster details page, click the alarm management tab and check whether ALM-12017 Insufficient Disk Capacity is generated in the alarm list.

      -  If yes, go to :ref:`2.b <alm_12007__en-us_topic_0191813896_li41496976164852>`.
      -  If no, go to :ref:`3 <alm_12007__en-us_topic_0191813896_li572522141314>`.

   b. .. _alm_12007__en-us_topic_0191813896_li41496976164852:

      Handle the alarm by following the instructions in :ref:`ALM-12017 Insufficient Disk Capacity <alm_12017>`.

   c. Wait 5 minutes and check whether the ALM-12017 Insufficient Disk Capacity alarm is cleared.

      If yes, go to :ref:`2.d <alm_12007__en-us_topic_0191813896_li33899481164916>`.

      If no, go to :ref:`3 <alm_12007__en-us_topic_0191813896_li572522141314>`.

   d. .. _alm_12007__en-us_topic_0191813896_li33899481164916:

      Wait 5 minutes and check whether the alarm is cleared.

      If yes, no further action is required.

      If no, go to :ref:`3 <alm_12007__en-us_topic_0191813896_li572522141314>`.

#. .. _alm_12007__en-us_topic_0191813896_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
