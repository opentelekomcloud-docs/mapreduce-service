:original_name: ALM-45450.html

.. _ALM-45450:

ALM-45450 ClickHouse Failed to Obtain a Temporary Agency Credential
===================================================================

.. note::

   This section is available for MRS 3.3.1-LTS or later version only.

Alarm Description
-----------------

After the cold-hot separation function and an agency are configured, the system checks the status of the temporary agency credential every minute. This alarm is generated when the the temporary agency credential fails to be obtained for three consecutive times.

This alarm is automatically cleared when the system successfully obtains the temporary agency credential.

Alarm Attributes
----------------

======== ============== ================== ============ ============
Alarm ID Alarm Severity Alarm Type         Service Type Auto Cleared
======== ============== ================== ============ ============
45450    Critical       Quality of service ClickHouse   Yes
======== ============== ================== ============ ============

Alarm Parameters
----------------

+----------------------+-------------+--------------------------------------------------------------------+
| Type                 | Parameter   | Description                                                        |
+======================+=============+====================================================================+
| Location Information | Source      | Specifies the cluster or system for which the alarm was generated. |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | ServiceName | Specifies the service for which the alarm was generated.           |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | RoleName    | Specifies the role for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+
|                      | HostName    | Specifies the host for which the alarm was generated.              |
+----------------------+-------------+--------------------------------------------------------------------+

Impact on the System
--------------------

The system cannot access OBS after the temporary agency credential expires. Operations such as reading and writing cold data in OBS cannot be performed on tables configured with cold and hot separation policies.

Possible Causes
---------------

-  The OBS parameters configured for ClickHouse are incorrect.
-  The IAM service is abnormal.

Handling Procedure
------------------

#. Check whether the cold and hot separation configuration is correct. If the configuration is incorrect, modify the configuration and restart the ClickHouse instance. Wait for 3 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`2 <alm-45450__li1314322683817>`.

**Collect fault information.**

2. .. _alm-45450__li1314322683817:

   On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

3. Expand the **Service** drop-down list, and select **ClickHouse** for the target cluster.

4. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the abnormal host, and click **OK**.

5. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

6. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
