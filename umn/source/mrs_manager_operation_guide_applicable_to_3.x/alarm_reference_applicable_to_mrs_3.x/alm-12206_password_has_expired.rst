:original_name: ALM-12206.html

.. _ALM-12206:

ALM-12206 Password Has Expired
==============================

Alarm Description
-----------------

The system checks whether a user password has expired at 1:00 a.m. every day. This alarm is generated when a user password has expired.

This alarm is cleared when the user password in the system is within the validity period.

.. note::

   This alarm applies only to MRS 3.3.1 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
12206    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------+--------------------------------------------------------------------+
| Type                   | Parameter   | Description                                                        |
+========================+=============+====================================================================+
| Location Information   | Source      | Specifies the cluster or system for which the alarm was generated. |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | ServiceName | Specifies the service for which the alarm was generated.           |
+------------------------+-------------+--------------------------------------------------------------------+
| Additional Information | Details     | Specifies that the username of password that has expired.          |
+------------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

The account cannot be used.

Possible Causes
---------------

The user password has expired.

Handling Procedure
------------------

**Change the user password.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. In the alarm list, expand the alarm details, and view and record the name of the user whose password has expired in additional information.
#. Change the user password that has expired.
#. If the DataArts Studio service is interconnected, check whether DataArts Studio jobs uses an expired user password. If yes, go to the DataArts Studio management center to change the password and execute the affected jobs again.
#. Check whether the alarm is automatically cleared after 1:00 a.m. the next day.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-12206__li39839699173731>`.

**Collect fault information.**

5. .. _alm-12206__li39839699173731:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

6. Select **Controller** for **Service** and click **OK**.

7. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

8. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
