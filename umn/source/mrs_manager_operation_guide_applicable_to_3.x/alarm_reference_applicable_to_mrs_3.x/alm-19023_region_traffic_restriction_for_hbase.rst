:original_name: ALM-19023.html

.. _ALM-19023:

ALM-19023 Region Traffic Restriction for HBase
==============================================

Alarm Description
-----------------

When the MetricController instance is installed for the HBase service, self-healing from hotspotting is automatically enabled. The alarm module checks whether there are regions whose request traffic is restricted due to hotspot issues in HBase every 120 seconds. This alarm is generated when the region where hotspot traffic is restricted is detected in HBase.

This alarm is cleared when the region is no longer a hotspot.

This alarm applies only to MRS 3.3.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
19023    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

=========== =======================================================
Parameter   Description
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

If the traffic of a hotspot region is restricted, the number of handlers for processing the requests in the region is limited. As a result, services requesting the region may slow down or retry upon failure.

Possible Causes
---------------

Too many requests are directed to a single region when the HBase service is accessed.

Handling Procedure
------------------

**Check whether there are too many requests in a single region of HBase.**

#. Log in to FusionInsight Manager, and Choose **O&M** > **Alarm** > **Alarms**.

#. .. _alm-19023__li864533612584:

   In **Additional Information** of **Region Traffic Restriction for HBase**, view the reported table name and region information.

#. On FusionInsight Manager, choose **Cluster** > **Service** > **HBase** and click the hyperlink on the right of HMaster web UI.

#. Click **Table Details** and adjust service configurations in the region where the table in :ref:`2 <alm-19023__li864533612584>` is deployed.

#. Wait a moment and then check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-19023__li16644173610580>`.

**Collect fault information.**

6.  .. _alm-19023__li16644173610580:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

7.  Expand the **Service** drop-down list, and select **HBase** for the target cluster.

8.  In the **Host** area, select the host where the HMaster instance is deployed.

9.  Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm will be automatically cleared.

Related Information
-------------------

None.
