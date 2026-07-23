:original_name: ALM-50231-1.html

.. _ALM-50231-1:

ALM-50231 Memory Used by the BE Process Page Table Entries Exceeds the Threshold
================================================================================

Alarm Description
-----------------

The system checks the percentage of node memory used by BE process page table entries (VmPTE) every 30 seconds. This alarm is generated when the percentage exceeds the threshold (15% by default).This alarm is cleared when the system detects that the percentage of node memory used by BE process page table entries is less than the threshold.

A page table is a data structure maintained by the operating system to manage mappings between physical memory and virtual memory. Each process has its own page table entries.

This alarm applies only to MRS 3.6.0-LTS and later versions.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
50231    Major          Yes
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

The available memory of the BE process decreases.

Possible Causes
---------------

A large amount of virtual memory has been allocated to user services, causing continuous increase in the memory consumed by the BE process's page table entries.

Handling Procedure
------------------

**Check whether the memory used by the page table entries of the BE process exceeds the threshold.**

#. Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. In the alarm list, view the role name and obtain the IP address of the instance in **Location** of the alarm whose ID is **50231**.

#. .. _alm-50231-1__en-us_topic_0000002516232789_en-us_topic_0000002434319780_li3863144110813:

   Choose **Thresholds**. In the displayed navigation pane, choose **Doris** > **CPU and Memory** > **BE VmPTE Node Memory Usage (BE)**. View and record the configured threshold of the alarm. The default threshold is 15%.

#. .. _alm-50231-1__en-us_topic_0000002516232789_en-us_topic_0000002434319780_li386424111819:

   Choose **Hosts**. In the host list, view the maximum memory of the host for which the alarm is generated and multiply the maximum memory by the alarm threshold obtained in :ref:`2 <alm-50231-1__en-us_topic_0000002516232789_en-us_topic_0000002434319780_li3863144110813>`. The obtained value is the VmPTE value of the BE process.

#. Choose **Cluster** > **Services** > **Doris** > **Instances**, click the BE instance for which the alarm is generated, click the **Chart** tab, select **CPU and Memory** under **Chart Category**, and check whether the value of the VmPTE metric in the **BE Memory Usage** chart exceeds the BE process VmPTE value obtained in :ref:`3 <alm-50231-1__en-us_topic_0000002516232789_en-us_topic_0000002434319780_li386424111819>`.

   -  If yes, go to :ref:`5 <alm-50231-1__en-us_topic_0000002516232789_en-us_topic_0000002434319780_li38645411388>`.
   -  If no, go to :ref:`7 <alm-50231-1__en-us_topic_0000002516232789_en-us_topic_0000002434319780_li148631141581>`.

#. .. _alm-50231-1__en-us_topic_0000002516232789_en-us_topic_0000002434319780_li38645411388:

   Stop new services based on your service requirements and restart the BE process.

#. After the services run for a period of time, choose **O&M** > **Alarm** > **Alarms**, and check whether this alarm is reported again.

   -  If yes, go to :ref:`7 <alm-50231-1__en-us_topic_0000002516232789_en-us_topic_0000002434319780_li148631141581>`.
   -  If no, no further action is required.

**Collect fault information.**

7.  .. _alm-50231-1__en-us_topic_0000002516232789_en-us_topic_0000002434319780_li148631141581:

    On MRS Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

8.  Expand the **Service** drop-down list, select **Doris** for the target cluster, and click **OK**.

9.  Click the edit icon in the upper right corner, and select a time span starting 10 minutes before and ending 10 minutes after when the alarm was generated. Then, click **Download** to collect the logs.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
