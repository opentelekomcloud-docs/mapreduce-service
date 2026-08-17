:original_name: ALM-19039.html

.. _ALM-19039:

ALM-19039 Average Number of StoreFiles per Store on a RegionServer Exceeds the Threshold
========================================================================================

Alarm Description
-----------------

The system checks the number of StoreFiles and the number of Stores of the HBase RegionServer instance every 30 seconds, divides the number of StoreFiles by the number of Stores to obtain the average value, and compares the average value with the threshold. By default, this alarm is generated when the average value exceeds the alarm threshold (**20** by default) for five consecutive times.

This alarm is cleared when the average number of StoreFiles per Store in the HBase RegionServer instance is less than or equal to the threshold.

.. note::

   This alarm applies only to MRS 3.6.0-LTS.1 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
19039    Major          Yes
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

If the average number of StoreFiles per Store on the RegionServer exceeds the threshold, it indicates that there are too many StoreFiles under a single Store on that RegionServer, which affects HBase service read operations. As a result, the read performance deteriorates, the Compaction task pressure is high, and write backpressure may occur.

Possible Causes
---------------

-  The cluster write pressure is too high, and the Compaction tasks are stacked.
-  Compaction tasks are not executed properly. For example, automatic Major Compaction is disabled, and Major Compaction is disabled or not manually executed.
-  The HBase region partitioning is improper, causing write operations to concentrate on several regions or the RegionServer.

Handling Procedure
------------------

#. Log in to Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing the alarm whose **Alarm ID** is **19039**, and view the service instance and host name in **Location**.

**Check the HBase Compaction task pressure.**

2. Check whether "ALM-19018 HBase Compaction Queue Size Exceeds the Threshold" is generated on the same node where the alarm is reported.

   -  If yes, go to :ref:`3 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li15979369259>`.
   -  If no, go to :ref:`5 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li19514153825119>`.

3. .. _alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li15979369259:

   Rectify the fault by following the handling procedure of "ALM-19018 HBase Compaction Queue Size Exceeds the Threshold".

4. Check whether the alarm is cleared a few minutes later.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li19514153825119>`.

**Check whether the HBase Compaction task is executed properly.**

5.  .. _alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li19514153825119:

    On Manager, choose **Cluster** > **Services** > **HBase** > **Configurations**, search for the parameter **hbase.hregion.majorcompaction** in the search box, and check whether the parameter value is 0.

    -  If yes, go to :ref:`6 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li15497868359>`.
    -  If no, go to :ref:`8 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li18976123135715>`.

6.  .. _alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li15497868359:

    If the value of **hbase.hregion.majorcompaction** is 0, automatic Major Compaction is disabled. In this case, the service O&M engineers need to align the Major Compaction execution time and preferentially select off-peak hours to ensure that the Major Compaction task is executed periodically.

    For the Major Compaction operation, you can run the following command in **hbase shell** to view the command examples of different compaction objects, and then manually perform the **major_compact** operation:

    .. code-block::

       help 'major_compact'

7.  After the Major Compaction task is executed, wait for several minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`8 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li18976123135715>`.

8.  .. _alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li18976123135715:

    On Manager, choose **Cluster** > **Services** > **HBase** > **Configurations**, enter **hbase.hstore.compaction.min** in the search box, and check whether the parameter value is greater than the alarm threshold (**20** by default).

    -  If yes, go to :ref:`9 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li342742494319>`.
    -  If no, go to :ref:`11 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li748224719108>`.

9.  .. _alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li342742494319:

    Minor Compaction is not performed because the number of StoreFiles per Store does not reach the threshold. The service O&M personnel need to evaluate service risks and parameter settings. Adjust the related configuration based on the site requirements and restart the RegionServer for the configuration to take effect.

10. Wait for a while and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li748224719108>`.

11. .. _alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li748224719108:

    Choose **Cluster** > **Services** > **HBase** > **Instances**, click the RegionServer instance for which the alarm is generated, and click the **Chart** tab. In the **Chart Category** area, choose **Queue**, and check whether the value of **Compaction Queue Size** is **0** in the **Queue Size of a RegionServer** chart.

    -  If yes, go to :ref:`12 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li16635193375616>`.
    -  If no, go to :ref:`14 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li253413154917>`.

12. .. _alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li16635193375616:

    Ensure that the Minor Compaction operation can be performed properly on the current cluster resources and run the following command in **hbase shell**:

    .. code-block::

       compaction_switch 'true'

    This command returns the previous status of the Compaction thread pool of each RegionServer. If "Servername 'false'" is returned, the Compaction task on the corresponding RegionServer is disabled.

13. After the command is executed, wait for a while and check whether this alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`14 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li253413154917>`.

**Check whether the HBase Region partitioning is proper.**

14. .. _alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li253413154917:

    On Manager, choose **Cluster** > **Services** > **HBase**. On the **Dashboard** page, click the hyperlink on the right of **HMaster Web UI** to go to the HBase web UI. In the **Region Servers** area on the **Home** page, click the name of the RegionServer for which the alarm is generated to go to the details page, click the **Storefile Metrics** tab in the **Regions** area, sort the values of **Num.Storefiles**, and record the table names whose values of **Num.Storefiles** exceed **20** in the **Region Name** column. The format of **Region Name** is as follows: "*Table name*,\ *startkey*,\ *Timestamp*,\ *encodedRegionName*."

15. Return to the **Home** page of the HBase web UI. In the **Tables** area, click one of the table names that are recorded to go to the table details page. In the **Table Regions** area, sort the values of **Num.Storefiles** and check whether there are regions with much more StoreFiles than other regions.

    -  If yes, go to :ref:`16 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li11853164193310>`.
    -  If no, go to :ref:`18 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li66014362013>`.

16. .. _alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li11853164193310:

    Run the following command in the **hbase shell** to split the region to balance its data distribution:

    .. code-block::

       split 'RegionName'

17. After the command is executed, wait for a while and check whether this alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`18 <alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li66014362013>`.

**Collect fault information.**

18. .. _alm-19039__en-us_topic_0000002523991716_en-us_topic_0000002518427320_li66014362013:

    On Manager, choose **O&M** > **Log** > **Download**.

19. Expand the **Service** drop-down list, and select **HBase** for the target cluster.

20. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

21. Send the collected fault logs to O&M personnel for help.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
