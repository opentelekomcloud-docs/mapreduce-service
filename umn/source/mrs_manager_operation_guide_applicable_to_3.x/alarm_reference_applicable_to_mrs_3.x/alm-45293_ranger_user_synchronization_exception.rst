:original_name: ALM-45293.html

.. _ALM-45293:

ALM-45293 Ranger User Synchronization Exception
===============================================

Alarm Description
-----------------

The system checks synchronization status of the UserSync process every 5 minutes. This alarm is generated when a synchronization exception occurs. This alarm is cleared when user synchronization becomes normal.

Alarm Attributes
----------------

======== ============== ================== ============ ============
Alarm ID Alarm Severity Alarm Type         Service Type Auto Cleared
======== ============== ================== ============ ============
45293    Major          Quality of service Ranger       Yes
======== ============== ================== ============ ============

Alarm Changes
-------------

=========== ======= =========== =================
Change Type Version Description Reason for Change
=========== ======= =========== =================
New         3.3.1   New alarm   New alarm
=========== ======= =========== =================

Alarm Parameters
----------------

+------------------------+-------------------+---------------------------------------------------------------------------------------------------+
| Type                   | Parameter         | Description                                                                                       |
+========================+===================+===================================================================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated.                                          |
+------------------------+-------------------+---------------------------------------------------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated.                                          |
+------------------------+-------------------+---------------------------------------------------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.                                             |
+------------------------+-------------------+---------------------------------------------------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.                                             |
+------------------------+-------------------+---------------------------------------------------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the trigger condition, that is, an exception occurs during Ranger user synchronization. |
+------------------------+-------------------+---------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

Unsynchronized users cannot access the native Ranger page and set permission policies for other users. As a result, some users may fail to access services that require Ranger permissions.

Possible Causes
---------------

The RangerAdmin instance is abnormal.

The UserSync instance is abnormal.

The LDAP service is abnormal.

Handling Procedure
------------------

**Check whether the UserSync is abnormal.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms** > **ALM-45293 Ranger User Synchronization Exception**. Check the location information of the alarm and view the host name of the instance for which the alarm is generated.

#. On MRS Manager, choose **Cluster** > **Services** > **Ranger** > **Instance**, select the UserSync instance on the host for which the alarm is generated, and check whether the instance status is abnormal.

   -  If yes, go to :ref:`3 <alm-45293__li09641391215>`.
   -  If no, go to :ref:`5 <alm-45293__li10964163913214>`.

#. .. _alm-45293__li09641391215:

   On MRS Manager, choose **Cluster** > **Services** > **Ranger**, click **Instances**, and click **UserSync**. On the displayed page, click **More** > **Restart Instance**, or restart the Ranger service.

#. Check whether the alarm is cleared in 5 to 10 minutes.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45293__li10964163913214>`.

**Check whether the RangerAdmin is abnormal.**

5. .. _alm-45293__li10964163913214:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms** to check whether alarm "ALM-45276 Abnormal RangerAdmin Status" is reported.

   -  If yes, go to :ref:`6 <alm-45293__li119731645112311>`.
   -  If no, go to :ref:`8 <alm-45293__li463216366256>`.

6. .. _alm-45293__li119731645112311:

   Rectify the fault by following the handling procedure of "ALM-45276 Abnormal RangerAdmin Status".

7. Check whether the alarm is cleared in 5 to 10 minutes.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-45293__li463216366256>`.

**Check whether the LDAP service is abnormal.**

8. .. _alm-45293__li463216366256:

   On MRS Manager, choose **O&M** > **Alarm** > **Alarms** to check whether alarm "ALM-25000 LdapServer Service Unavailable" is reported.

   -  If yes, go to :ref:`9 <alm-45293__li17632103632510>`.
   -  If no, go to :ref:`11 <alm-45293__d0e44409>`.

9.  .. _alm-45293__li17632103632510:

    Clear the alarm according to the handling procedure of "ALM-25000 LdapServer Service Unavailable".

10. Check whether the alarm is cleared in 5 to 10 minutes.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-45293__d0e44409>`.

**Collect fault information.**

11. .. _alm-45293__d0e44409:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

12. Expand the **Service** drop-down list, and select **Ranger** for the target cluster.

13. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
