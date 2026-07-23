:original_name: ALM-18029.html

.. _ALM-18029:

ALM-18029 Total Size of Files in the Yarn-nm-state Directory of NodeManager Exceeds the Threshold
=================================================================================================

Alarm Description
-----------------

NodeManager checks every 30 seconds if the total size of files in the **yarn-nm-state** directory on the node where the instance is deployed exceeds 100 MB. This alarm is triggered when the total size exceeds 100 MB.

This alarm is cleared when the total size of files in the **yarn-nm-state** directory on the node where the NodeManager instance is deployed is less than 100 MB.

.. note::

   This alarm applies only to MRS 3.6.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
18029    Major          Yes
======== ============== ============

Alarm Parameters
----------------

+------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------+
| Type                   | Parameter         | Description                                                                                                                       |
+========================+===================+===================================================================================================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated.                                                                          |
+------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated.                                                                          |
+------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.                                                                             |
+------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.                                                                             |
+------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------+
| Additional Information | Trigger Condition | The total size of files in the **yarn-nm-state** directory on the node where the NodeManager instance is deployed exceeds 100 MB. |
+------------------------+-------------------+-----------------------------------------------------------------------------------------------------------------------------------+

Impact on the System
--------------------

A large number of useless Container heartbeats may be generated, affecting ResourceManager's overall task scheduling.

Possible Causes
---------------

The Container information of the NodeManager node is not cleared.

Handling Procedure
------------------

**Clear the residual Container information on the NodeManager node.**

#. .. _alm-18029__en-us_topic_0000002204705717_en-us_topic_0000002137741664_li166717351206:

   Log in to MRS Manager, and choose **O&M** > **Alarm** > **Alarms**. Click the hostname reported in the alarm details to obtain the service IP address of the host.

#. Choose **Cluster** > **Services** > Yarn > **Instances**. Select the NodeManager instances with the same IP address as the one you obtained in :ref:`1 <alm-18029__en-us_topic_0000002204705717_en-us_topic_0000002137741664_li166717351206>`, choose **More** > **Stop Instance**, and stop the instance as prompted.

3. Log in to the host for which the alarm is reported as user **root**, using the service IP address obtained in :ref:`1 <alm-18029__en-us_topic_0000002204705717_en-us_topic_0000002137741664_li166717351206>`, and run the following command to switch to user **omm**:

   **su - omm**

4. Run the following command to clear files in the **yarn-nm-state** directory:

   **rm -rf ${SRV_HOME}/tmp/yarn-nm-recovery/yarn-nm-state/\***

5. On MRS Manager, choose **Cluster** > **Services** > **Yarn** > **Instances**, check the NodeManager instance for which the alarm is reported, click **Start Instance**, and start the instance as prompted.

6. Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-18029__en-us_topic_0000002204705717_en-us_topic_0000002137741664_li10805181583414>`.

7. .. _alm-18029__en-us_topic_0000002204705717_en-us_topic_0000002137741664_li10805181583414:

   Contact O&M personnel to rectify the fault.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
