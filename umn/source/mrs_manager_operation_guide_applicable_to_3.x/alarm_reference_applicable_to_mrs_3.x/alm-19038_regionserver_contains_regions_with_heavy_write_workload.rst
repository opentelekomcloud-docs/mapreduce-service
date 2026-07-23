:original_name: ALM-19038.html

.. _ALM-19038:

ALM-19038 RegionServer Contains Regions with Heavy Write Workload
=================================================================

Alarm Description
-----------------

Every 30 seconds, the system checks the number of requests blocked on the HBase RegionServer instance due to MemStore reaching its upper limit, and compares this number against a threshold. By default, if the number of blocked requests exceeds the alarm threshold (450 by default) for five consecutive times, this alarm is generated.

This alarm is cleared when the number of requests blocked by the HBase RegionServer due to MemStore reaching its upper limit falls to or below the defined threshold.

.. note::

   This alarm applies only to MRS 3.6.0-LTS or later.

Alarm Attributes
----------------

======== ============== ================== ============ ============
Alarm ID Alarm Severity Alarm Type         Service Type Auto Cleared
======== ============== ================== ============ ============
19038    Minor          Quality of service HBase        Yes
======== ============== ================== ============ ============

Alarm Parameters
----------------

+------------------------+-------------------+----------------------------------------------------------+
| Type                   | Parameter         | Description                                              |
+========================+===================+==========================================================+
| Location Information   | Source            | Specifies the cluster for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | ServiceName       | Specifies the service for which the alarm was generated. |
+------------------------+-------------------+----------------------------------------------------------+
|                        | RoleName          | Specifies the role for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
|                        | HostName          | Specifies the host for which the alarm was generated.    |
+------------------------+-------------------+----------------------------------------------------------+
| Additional Information | Trigger Condition | Specifies the alarm triggering condition.                |
+------------------------+-------------------+----------------------------------------------------------+

Impact on the System
--------------------

Write requests are blocked by the HBase RegionServer instance due to MemStore reaching its upper limit, and overall write performance degrades.

Possible Causes
---------------

The HBase client service may be experiencing write request overload or hotspot issues.

Handling Procedure
------------------

**Check whether there is the write request overload or hotspot issue in the HBase client service.**

#. .. _alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li23652015192818:

   Log in to MRS Manager and choose **O&M** > **Alarm** > **Alarms**. In the **Location** field of the alarm details, record the host name of the RegionServer instance for which this alarm is generated.

#. .. _alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li2941154513215:

   On MRS Manager, choose **O&M** > **Log** > **Online Search**. Enter **RegionTooBusy** in the **Search Content** text box, select **HBase** for **Service**, select the host obtained in :ref:`1 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li23652015192818>` for **Host Scope**, and click **Search**. In the search result, view and record the name of the regions with heavy write workload.

   -  If the search result shows that **RegionTooBusy** is frequently reported for a single region, the HBase client service is experiencing write request hotspots. In this case, go to :ref:`3 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li717124754311>`.
   -  If the search result shows that **RegionTooBusy** is reported for multiple regions, the HBase client service is experiencing write request overload. In this case, go to :ref:`4 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li1510812558910>`.

#. .. _alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li717124754311:

   If the HBase client service is experiencing write request hotspots, split the region.

   a. Log in to the node where the HBase client is deployed, configure environment variables, and authenticate the user.

      **cd** *Client installation directory*

      **source bigdata_env**

      **kinit** *Component service user* (If Kerberos authentication is disabled for the cluster (the cluster is in normal mode), skip this step.)

   b. Run the following command to split the region:

      **split '**\ *regionName*\ **'**

      *regionName* is the region name obtained in :ref:`2 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li2941154513215>`. After the region is split, perform :ref:`5 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li4503917161319>`.

#. .. _alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li1510812558910:

   If the HBase client service is experiencing write request overload, split the table or modify the memory size of the flush disk.

   -  Split the table.

      a. On MRS Manager, choose **Cluster** > **Services** > **HBase**. On the **Dashboard** page, click the hyperlink **HMaster(xxx,Active)** on the right of **HMaster Web UI** to go to the HBase web UI.

      b. In the **Base Stats** area for **Region Servers**, click the RegionServer for which the alarm is generated. In the **Regions** area of the RegionServer, search for the region name obtained in :ref:`2 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li2941154513215>`. The content before the first separator in the search result is the HBase table name. For example, if the search result is **hbase,\ xxxx**, the HBase table name is **hbase**.

      c. Return to the HBase web UI home page. In the **Tables** area, click the table name to access the table information page. In the **Table Regions** area, view the **ReadRequests**, **WriteRequests**, **Start Key**, and **End Key** columns to check whether the table is properly pre-partitioned.

         -  If yes, go to :ref:`7 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li42224042151734>`.
         -  If no, go to :ref:`4.d <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li871619321163>`.

      d. .. _alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li871619321163:

         If a table is improperly pre-partitioned and the service's partitioning strategy cannot be promptly corrected, split the table to avoid the **RegionTooBusy** issue.

         #. Log in to the node where the HBase client is deployed, configure environment variables, and authenticate the user.

            **cd** *Client installation directory*

            **source bigdata_env**

            **kinit** *Component service user* (If Kerberos authentication is disabled for the cluster (the cluster is in normal mode), skip this step.)

         #. Run the following command to split the table:

            **split '**\ *tableName'*

            After the table is split, go to :ref:`5 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li4503917161319>`.

   -  Modify the memory size of the flush disk.

      a. On MRS Manager, choose **Cluster** > **Services** > **HBase** > **Configurations**, search for **hbase.hregion.memstore.flush.size** in the search box, and increase its value to adjust the MemStore memory limit for blocking write operations. It is recommended that the value be less than or equal to 256 MB. Otherwise, the RegionServer memory usage is affected.

         HBase calculates the memory limit for blocking write operations using the following formula: hbase.hregion.memstore.block.multiplier \* hbase.hregion.memstore.flush.size

      b. Click **Save**. Click **Instances**, select the affected RegionServer instances, choose **More** > **Restart Instance**. Enter the password of the user and click **OK** to restart the RegionServer instances to apply the configurations.

         After the RegionServer instances restarts, perform :ref:`5 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li4503917161319>`.

#. .. _alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li4503917161319:

   Wait 5 minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li11161623152819>`.

#. .. _alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li11161623152819:

   Perform :ref:`1 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li23652015192818>` to :ref:`4 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li1510812558910>` again, wait for 5 minutes, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li42224042151734>`.

**Collect fault information.**

7.  .. _alm-19038__en-us_topic_0000002483992846_en-us_topic_0000002457131017_li42224042151734:

    On MRS Manager, choose **O&M** > **Log** > **Download**.

8.  Expand the **Service** drop-down list, and select **HBase** for the target cluster.

9.  Click the edit icon in the upper right corner, and select a time span starting 10 minutes before and ending 10 minutes after when the alarm was generated. Then, click **Download** to collect the logs.

10. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
