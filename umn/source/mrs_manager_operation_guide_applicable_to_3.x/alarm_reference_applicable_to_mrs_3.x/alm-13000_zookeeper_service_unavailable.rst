:original_name: ALM-13000.html

.. _ALM-13000:

ALM-13000 ZooKeeper Service Unavailable
=======================================

Description
-----------

The system checks the ZooKeeper service status every 60 seconds. This alarm is generated when the ZooKeeper service is unavailable.

This alarm is cleared when the ZooKeeper service recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
13000    Critical       Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

ZooKeeper cannot provide coordination services for upper layer components and the components that depend on ZooKeeper may not run properly.

Possible Causes
---------------

-  The DNS is installed on the ZooKeeper node.
-  The network is faulty.
-  The KrbServer service is abnormal.
-  The ZooKeeper instance is abnormal.
-  The disk capacity is insufficient.

Procedure
---------

**Check the DNS.**

#. Check whether the DNS is installed on the node where the ZooKeeper instance is located. On the Linux node where the ZooKeeper instance is located, run the **cat /etc/resolv.conf** command to check whether the file is empty.

   -  If yes, go to :ref:`2 <alm-13000__li76816175112>`.
   -  If no, go to :ref:`3 <alm-13000__li86969116511>`.

#. .. _alm-13000__li76816175112:

   Run the **service named status** command to check whether the DNS is started.

   -  If yes, go to :ref:`3 <alm-13000__li86969116511>`.
   -  If no, go to :ref:`5 <alm-13000__li42741615115119>`.

#. .. _alm-13000__li86969116511:

   Run the **service named stop** command to stop the DNS service. If "Shutting down name server BIND waiting for named to shut down (28s)" is displayed, the DNS service is stopped successfully. Comment out the content (if any) in **/etc/resolv.conf**.

#. On the **O&M > Alarm > Alarms** tab, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-13000__li42741615115119>`.

**Check the network status.**

5. .. _alm-13000__li42741615115119:

   On the Linux node where the ZooKeeper instance is located, run the **ping** command to check whether the host names of other nodes where the ZooKeeper instance is located can be pinged successfully.

   -  If yes, go to :ref:`9 <alm-13000__li26784425155523>`.
   -  If no, go to :ref:`6 <alm-13000__li1227471525111>`.

6. .. _alm-13000__li1227471525111:

   Modify the IP addresses in **/etc/hosts** and add the host name and IP address mapping.

7. Run the **ping** command again to check whether the host names of other nodes where the ZooKeeper instance is located can be pinged successfully.

   -  If yes, go to :ref:`8 <alm-13000__li129021555116>`.
   -  If no, go to :ref:`23 <alm-13000__li42883384155523>`.

8. .. _alm-13000__li129021555116:

   On the **O&M > Alarm > Alarms** tab, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-13000__li26784425155523>`.

**Check the KrbServer service status (Skip this step if the normal mode is used).**

9.  .. _alm-13000__li26784425155523:

    On MRS Manager, choose **Cluster >** *Name of the desired cluster* **> Services**.

10. Check whether the KrbServer service is normal.

    -  If yes, go to :ref:`13 <alm-13000__li21042948155523>`.
    -  If no, go to :ref:`11 <alm-13000__li45270224155523>`.

11. .. _alm-13000__li45270224155523:

    Perform operations based on "ALM-25500 KrbServer Service Unavailable" and check whether the KrbServer service is recovered.

    -  If yes, go to :ref:`12 <alm-13000__li4125272155523>`.
    -  If no, go to :ref:`23 <alm-13000__li42883384155523>`.

12. .. _alm-13000__li4125272155523:

    On the **O&M > Alarm > Alarms** tab, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-13000__li21042948155523>`.

**Check the ZooKeeper service instance status.**

13. .. _alm-13000__li21042948155523:

    On MRS Manager, choose **Cluster >** *Name of the desired cluster* **> Services** > **ZooKeeper** > **quorumpeer**.

14. Check whether the ZooKeeper instances are normal.

    -  If yes, go to :ref:`18 <alm-13000__li253728155523>`.
    -  If no, go to :ref:`15 <alm-13000__li36165444155523>`.

15. .. _alm-13000__li36165444155523:

    Select instances whose status is not good, and choose **More** > **Restart Instance**.

16. Check whether the instance status is good after restart.

    -  If yes, go to :ref:`17 <alm-13000__li65308695155523>`.
    -  If no, go to :ref:`18 <alm-13000__li253728155523>`.

17. .. _alm-13000__li65308695155523:

    On the **O&M > Alarm > Alarms** tab, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`18 <alm-13000__li253728155523>`.

**Check disk status.**

18. .. _alm-13000__li253728155523:

    On MRS Manager, choose **Cluster >** *Name of the desired cluster* **> Service** > **ZooKeeper** > **quorumpeer**, and check the node host information of the ZooKeeper instance.

19. On MRS Manager, click **Host**.

20. In the **Disk** column, check whether the disk space of each node where ZooKeeper instances are located is insufficient (disk usage exceeds 80%).

    -  If yes, go to :ref:`21 <alm-13000__li23393056155523>`.
    -  If no, go to :ref:`23 <alm-13000__li42883384155523>`.

21. .. _alm-13000__li23393056155523:

    Expand disk capacity. For details, see "ALM-12017 Insufficient Disk Capacity".

22. On the **O&M > Alarm > Alarms** tab, check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`23 <alm-13000__li42883384155523>`.

**Collect fault information.**

23. .. _alm-13000__li42883384155523:

    On the MRS Manager portal, choose **O&M** > **Log > Download**.

24. Select the following nodes in the required cluster from the **Service**: (KrbServer logs do not need to be downloaded in normal mode.)

    -  ZooKeeper
    -  KrbServer

25. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

26. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001582807793.png
