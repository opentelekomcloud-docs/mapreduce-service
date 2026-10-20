:original_name: ALM-19040.html

.. _ALM-19040:

ALM-19040 Abnormal Regions in HBase
===================================

Alarm Description
-----------------

The system checks whether there are abnormal regions in HBase every 60 seconds. The abnormal regions include regions in **ABNORMALLY_CLOSED** state (abnormally closed regions), **FAILED_OPEN** state (regions that fail to be opened by RegionServer), and **FAILED_CLOSE** state (regions that fail to be closed by RegionServer). This alarm is generated when abnormal regions are detected in HBase.

This alarm is cleared when there is no abnormal region in HBase.

.. note::

   This alarm applies only to MRS 3.6.0-LTS.1 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
19040    Major          Yes
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
| Additional Information | Threshold   | Specifies the threshold for generating the alarm.        |
+------------------------+-------------+----------------------------------------------------------+

Impact on the System
--------------------

The region in abnormal state may not go online as expected, and an error may be reported when services access the region.

Possible Causes
---------------

The HBase region fails to go online or offline due to an exception.

Handling Procedure
------------------

**Check whether there are abnormal regions in HBase.**

#. Log in to Manager, choose **Cluster** > **Services** > **HBase** > **Chart**. In the **Chart Category** area, click **Service**, and check the number of abnormal regions in the **Number of Abnormal Regions** chart.

#. Click **Dashboard** and click the hyperlink on the right of **HMaster Web UI** to access the HBase web UI.

#. On the **User Tables** tab page in the **Tables** area, sort the values in the **Other** column and check whether there are values that are not **0**.

   -  If yes, go to :ref:`4 <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li1196714310557>`.
   -  If no, go to :ref:`8 <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li16644173610580>`.

#. .. _alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li1196714310557:

   Locate the row where the value of **Other** is not **0** and click the corresponding table name in the **Name** column to go to the table details page. In the **Table Regions** area, click the **Base Stats** tab and check whether there are multiple regions whose **Region State** is **ABNORMALLY_CLOSED**.

   -  If yes, go to :ref:`5 <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li1619815368593>`.
   -  If no, go to :ref:`7 <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li136150591438>`.

#. .. _alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li1619815368593:

   If possible, perform the following operations in **hbase shell** to bring the table region online again:

   a. Disable the HBase table.

      **disable** '*Table name*'

   b. Enable the HBase table.

      **enable** '*Table name*'

#. After the table region is brought online, wait for several minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li16644173610580>`.

#. .. _alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li136150591438:

   Since only a few regions in this table are abnormal, you can use the HBCK tool to restore the table.

   a. .. _alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li2870141313132:

      On the HBase web UI, choose **Procedure & Locks** in the navigation pane. In the **Procedures** area, check whether there are regions whose procedures are not updated for a long time.

      -  If yes, go to :ref:`7.b <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li198934151753>`.
      -  If no, go to :ref:`8 <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li16644173610580>`.

   b. .. _alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li198934151753:

      Log in to the node where the HBase client is installed as the client installation user and run the following commands to configure environment variables and authenticate the user:

      **cd** *Client installation directory*

      **source bigdata_env**

      **kinit hbase** (Skip this step if Kerberos authentication is disabled for the cluster (the cluster is in normal mode).)

   c. Run the following command to release the procedure lock:

      **hbase hbck -j** *Client installation directory*\ **/HBase/hbase/tools/hbase-hbck2-*.jar bypass -o** *pid*

      *pid* is the Procedure ID in the **Id** column in the Procedures area in :ref:`7.a <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li2870141313132>`.

   d. After the procedure lock is released, check whether the **State** of the region is **RUNNABLE(Bypass)** in the **Procedures** area mentioned in :ref:`7.a <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li2870141313132>`.

      -  If yes, go to :ref:`7.e <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li1811713714246>`.
      -  If no, go to :ref:`7.g <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li1023714272271>`.

   e. .. _alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li1811713714246:

      On Manager, choose **Cluster** > **Services** > **HBase**. In the upper right corner of the **Dashboard** page, choose **More** > **Perform HMaster Switchover**, enter the current user password, and click **OK** to perform an HMaster active/standby switchover.

   f. After the HMaster active/standby switchover is successful, wait for several minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`7.g <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li1023714272271>`.

   g. .. _alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li1023714272271:

      Run the following command to set the region status to **CLOSED**:

      **hbase hbck -j** *Client installation directory*\ **/HBase/hbase/tools/hbase-hbck2-*.jar setRegionState** *RegionName* **CLOSED**

   h. Run the following command to manually bring the region online again:

      **hbase hbck -j** *Client installation directory*\ **/HBase/hbase/tools/hbase-hbck2-*.jar assigns** *RegionName*

   i. Log in to the HBase web UI, choose **Procedure & Locks** in the navigation pane, and check whether there is a procedure for bringing a region online.

      -  If yes, go to :ref:`7.j <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li104763603618>`.
      -  If no, go to :ref:`8 <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li16644173610580>`.

   j. .. _alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li104763603618:

      In the navigation pane, choose **Home**. In the **Tables** area, click the **User Tables** tab and check whether all values in the **Other** column are **0**.

      -  If yes, go to :ref:`7.k <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li51133623714>`.
      -  If no, go to :ref:`8 <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li16644173610580>`.

   k. .. _alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li51133623714:

      On Manager, choose **Cluster** > **Services** > **HBase** > **Chart**. In the **Chart Category** area, click **Service** and check whether there are abnormal regions in the **Number of Abnormal Regions** chart.

      -  If yes, go to :ref:`8 <alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li16644173610580>`.
      -  If no, no further action is required.

**Collect fault information.**

8.  .. _alm-19040__en-us_topic_0000002555352257_en-us_topic_0000002523932456_li16644173610580:

    On Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

9.  Expand the **Service** drop-down list, and select **HBase** for the target cluster.

10. In the **Host** area, select the host where the HMaster instance is deployed.

11. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

12. Send the collected fault logs to O&M personnel for help.

Alarm Clearance
---------------

This alarm will be automatically cleared.

Related Information
-------------------

None.
