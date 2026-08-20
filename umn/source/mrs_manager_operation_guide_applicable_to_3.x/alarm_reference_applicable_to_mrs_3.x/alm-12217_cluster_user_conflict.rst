:original_name: ALM-12217.html

.. _ALM-12217:

ALM-12217 Cluster User Conflict
===============================

Alarm Description
-----------------

The system checks whether the MRS Manager users conflict with OS users every two hours. This alarm is generated when a Manager user created in the cluster conflicts with an OS user on the node.

This alarm is cleared when no user conflict is detected during the subsequent check period.

.. note::

   This alarm applies only to MRS 3.6.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12217    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------+----------------------------------------------------------+
| Type                   | Parameter   | Description                                              |
+========================+=============+==========================================================+
| Location Information   | Source      | Specifies the cluster for which the alarm was generated. |
+------------------------+-------------+----------------------------------------------------------+
|                        | ServiceName | Specifies the service for which the alarm was generated. |
+------------------------+-------------+----------------------------------------------------------+
|                        | RoleName    | Specifies the role for which the alarm was generated.    |
+------------------------+-------------+----------------------------------------------------------+
|                        | HostName    | Specifies the host for which the alarm was generated.    |
+------------------------+-------------+----------------------------------------------------------+
| Additional Information | Details     | Specifies alarm details.                                 |
+------------------------+-------------+----------------------------------------------------------+

Impact on the System
--------------------

-  Service authentication in components may fail, adversely affecting the service and process status.
-  Job submission on components may fail or jobs may run with unexpected issues.

Possible Causes
---------------

The user created on MRS Manager uses the same username as the OS user.

Handling Procedure
------------------

**Check whether there are user conflicts.**

#. Log in to MRS Manager, click **O&M**, and choose **Alarm** > **Alarms** to view the alarm details. In the **Location** column, check the name of the host for which the alarm is generated. Click the host name to view its IP address.

#. Log in to the host for which the alarm is generated as user **omm**.

#. Run the following command to obtain the OS users created on the current host and check whether there are OS users who use the same usernames as the Manager users in the cluster:

   **cut -d: -f1 /etc/passwd**

   -  If yes, go to :ref:`4 <alm-12217__en-us_topic_0000002487840004_en-us_topic_0000002450412321_li58248814610>`.
   -  If no, go to :ref:`6 <alm-12217__en-us_topic_0000002487840004_en-us_topic_0000002450412321_li1411651534617>`.

#. .. _alm-12217__en-us_topic_0000002487840004_en-us_topic_0000002450412321_li58248814610:

   If the current cluster contains OS users with usernames identical to those of Manager users, review the user list provided in the additional alarm information to identify the users and delete either the OS users or the Manager users as appropriate.

   Multiple conflicting users in the additional information are separated by spaces.

#. After resolving the user conflicts, wait for the next check period and check whether this alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12217__en-us_topic_0000002487840004_en-us_topic_0000002450412321_li1411651534617>`.

**Collect fault information.**

6. .. _alm-12217__en-us_topic_0000002487840004_en-us_topic_0000002450412321_li1411651534617:

   On MRS Manager, click **O&M**. On the displayed page, choose **Log** > **Download**.

7. Select **OmmServer** and **NodeAgent** for **Service**. Select the host name recorded in the alarm location information for **Hosts**.

8. Click the edit icon in the upper right corner, and select a time span starting 10 minutes before and ending 10 minutes after when the alarm was generated. Then, click **Download** to collect the logs.

9. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
