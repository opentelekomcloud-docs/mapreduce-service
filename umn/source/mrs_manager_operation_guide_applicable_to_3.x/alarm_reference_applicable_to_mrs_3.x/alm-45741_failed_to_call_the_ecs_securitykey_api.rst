:original_name: ALM-45741.html

.. _ALM-45741:

ALM-45741 Failed to Call the ECS securitykey API
================================================

Alarm Description
-----------------

Guardian caches the temporary AK/SK of the ECS agency. When the cache does not exist or is about to expire, Guardian calls the securitykey API of ECS to update the AK/SK. This alarm is generated when calling to the API fails.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45741    Major          Yes
======== ============== ============

Alarm Parameters
----------------

=========== ========================================================
Parameter   Description
=========== ========================================================
Source      Specifies the cluster for which the alarm was generated.
ServiceName Specifies the service for which the alarm was generated.
RoleName    Specifies the role for which the alarm was generated.
HostName    Specifies the host for which the alarm was generated.
=========== ========================================================

Impact on the System
--------------------

The task may fail to obtain the temporary AK/SK for accessing OBS. As a result, the task cannot access OBS.

Possible Causes
---------------

-  No ECS agency is bound to the cluster.
-  An underlying interface of ECS is abnormal.

Handling Procedure
------------------

**Check whether an agency is bound to the cluster.**

#. Log in to the MRS console.

#. In the navigation pane on the left, choose **Clusters** > **Active Clusters**. On the page that is displayed, click the cluster name to go to its overview page. Then, check whether the cluster is bound to an agency in the O&M management area.

   -  If yes, go to :ref:`4 <alm-45741__li16749195915615>`.
   -  If no, go to :ref:`3 <alm-45741__li14580102410349>`.

#. .. _alm-45741__li14580102410349:

   Click **Manage Agency**. On the page that is displayed, rebind the cluster to an agency. Then check whether the alarm is cleared a few minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-45741__li16749195915615>`.

**Collect fault information.**

4. .. _alm-45741__li16749195915615:

   On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

5. Expand the **Service** drop-down list, and select **Guardian** for the target cluster.

6. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001971781990.png
