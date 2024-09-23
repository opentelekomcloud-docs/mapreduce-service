:original_name: ALM-45652.html

.. _ALM-45652:

ALM-45652 Flink Service Unavailable
===================================

This section applies to MRS 3.3.0 or later.

Alarm Description
-----------------

The alarm module checks the Flink status every 60 seconds. This alarm is generated when the Flink service is unavailable. This alarm is cleared when the Flink service recovers.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
45652    Critical       Yes
======== ============== ============

Alarm Parameters
----------------

=========== =======================================================
Parameter   Description
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the job for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

FlinkServer and the Flink client cannot be used to submit Flink jobs.

Possible Causes
---------------

The ZooKeeper, HDFS, Yarn, KrbServer, or DBService service on which Flink depends is unavailable.

Handling Procedure
------------------

**Check whether the ZooKeeper service on which Flink depends is abnormal.**

#. Log in to FusionInsight Manager and choose **O&M** > **Alarm** > **Alarms**.

#. In the alarm list, check whether "ALM-13000 ZooKeeper Service Unavailable" exists.

   -  If yes, go to :ref:`3 <alm-45652__li16785184716596>`.
   -  If no, go to :ref:`5 <alm-45652__li936635985913>`.

#. .. _alm-45652__li16785184716596:

   Handle the alarm by referring to "ALM-13000 ZooKeeper Service Unavailable."

#. After the alarm is cleared, wait a few minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-45652__li936635985913>`.

**Check whether the HDFS service on which Flink depends is abnormal.**

5. .. _alm-45652__li936635985913:

   On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**.

6. In the alarm list, check whether "ALM-14000 HDFS Service Unavailable" exists.

   -  If yes, go to :ref:`7 <alm-45652__li14366125925911>`.
   -  If no, go to :ref:`9 <alm-45652__li1540834513593>`.

7. .. _alm-45652__li14366125925911:

   Handle the alarm by referring to "ALM-14000 HDFS Service Unavailable."

8. After the alarm is cleared, wait a few minutes and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-45652__li1540834513593>`.

**Check whether the Yarn service on which Flink depends is abnormal.**

9.  .. _alm-45652__li1540834513593:

    On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**.

10. In the alarm list, check whether "ALM-18000 Yarn Service Unavailable" exists.

    -  If yes, go to :ref:`11 <alm-45652__li1240810456591>`.
    -  If no, go to :ref:`13 <alm-45652__li10537624124112>`.

11. .. _alm-45652__li1240810456591:

    Handle the alarm by referring to "ALM-18000 Yarn Service Unavailable."

12. After the alarm is cleared, wait a few minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-45652__li10537624124112>`.

**Check whether the KrbServer service on which Flink depends is abnormal.**

13. .. _alm-45652__li10537624124112:

    On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**.

14. In the alarm list, check whether "ALM-25500 KrbServer Service Unavailable" exists.

    -  If yes, go to :ref:`15 <alm-45652__li1053752412412>`.
    -  If no, go to :ref:`17 <alm-45652__li1957661133312>`.

15. .. _alm-45652__li1053752412412:

    Handle the alarm by referring to "ALM-25500 KrbServer Service Unavailable."

16. After the alarm is cleared, wait a few minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`17 <alm-45652__li1957661133312>`.

**Check whether the DBService service on which Flink depends is abnormal.**

17. .. _alm-45652__li1957661133312:

    On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**.

18. In the alarm list, check whether "ALM-27001 DBService Service Unavailable" exists.

    -  If yes, go to :ref:`19 <alm-45652__li1857611153310>`.
    -  If no, go to :ref:`21 <alm-45652__li4749473185459>`.

19. .. _alm-45652__li1857611153310:

    Handle the alarm by referring to "ALM-27001 DBService Service Unavailable."

20. After the alarm is cleared, wait a few minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`21 <alm-45652__li4749473185459>`.

**Collect fault information.**

21. .. _alm-45652__li4749473185459:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

22. Expand the **Service** drop-down list, and select **Flink** for the target cluster.

23. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 30 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

24. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.

.. |image1| image:: /_static/images/en-us_image_0000002008248613.png
