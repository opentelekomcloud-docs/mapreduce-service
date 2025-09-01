:original_name: ALM-50230.html

.. _ALM-50230:

ALM-50230 Doris BE Cannot Connect to OBS
========================================

Alarm Description
-----------------

The system checks whether the connection between the Doris BE nodes and OBS is available every 30 seconds. This alarm is generated when the connection status code is not 0.

This alarm is cleared when the connection status code is 0.

This alarm applies only to MRS 3.3.1 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50230    Critical       Yes
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
|                        | RoleName    | Specifies the role for which the alarm was generated.              |
+------------------------+-------------+--------------------------------------------------------------------+
|                        | HostName    | Specifies the host for which the alarm was generated.              |
+------------------------+-------------+--------------------------------------------------------------------+
| Additional Information | Detail      | Specifies the alarm triggering condition.                          |
+------------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

Some functions of Doris are unavailable, for example, cold-hot separation and Hive OBS Catalog.

Possible Causes
---------------

-  The obtained AK/SK is invalid.
-  This alarm is generated when OBS connection fails.

Handling Procedure
------------------

**Determine the cause.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. In the alarm list, view the role name and obtain the IP address of the instance in **Location** of the alarm whose ID is **50230**, and check the **CurrentValue** in **Additional Information**.

   -  If **CurrentValue** is **2**, the obtained AK/SK is invalid. Go to :ref:`2 <alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li38093403127>`.
   -  If **CurrentValue** is **3**, OBS fails to be connected. Go to :ref:`7 <alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li1843117951716>`.

**The obtained AK/SK is invalid.**

2. .. _alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li38093403127:

   Log in to the MRS Service console, move the cursor on the username in the upper right corner, and choose **My Credentials**.

3. Click **Access Keys** and check whether **Status** of the target key is **Enabled**.

   -  If yes, go to :ref:`4 <alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li1380974061214>`.
   -  If no, click **Enable** in the **Operation** column of the row containing the key.

4. .. _alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li1380974061214:

   Click **Delete** in the row where the key is to delete the key. Click **Create Access Key** and click **OK**. Download the new access key and obtain the AK and SK.

5. Set the **obs.access_key** and **obs.secret_key** parameters to the obtained AK/SK.

6. Wait for about 1 minute, log in to MRS Manager, choose **O&M** > **Alarm** > **Alarms**, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li1843117951716>`.

**Failed to connect to OBS.**

7.  .. _alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li1843117951716:

    Check whether the network connection between the cluster and OBS is normal.

    -  If yes, go to :ref:`8 <alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li1443210921719>`.
    -  If no, go to :ref:`12 <alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li8194169123519>`.

8.  .. _alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li1443210921719:

    Log in to the MRS management console. In the service list, choose **Identity and Access Management**. Click **Agencies** in the navigation pane. In the agency list, click the agency name configured for the MRS cluster.

9.  Click **Permissions** and click the name of each policy in the permission list.

10. In the **Content** area, search for **Action** and check whether **obs** is contained.

    -  If yes, go to :ref:`12 <alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li8194169123519>`.
    -  If no, go to :ref:`11 <alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li13555132516119>`.

11. .. _alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li13555132516119:

    Create an OBS permission policy by following the instructions provided in the guide for configuring doris cold and hot data separation. Wait for about 15 to 20 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li8194169123519>`.

12. .. _alm-50230__en-us_topic_0000001867406297_en-us_topic_0000001819654780_li8194169123519:

    Contact O&M personnel for fault diagnosis and rectification.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
