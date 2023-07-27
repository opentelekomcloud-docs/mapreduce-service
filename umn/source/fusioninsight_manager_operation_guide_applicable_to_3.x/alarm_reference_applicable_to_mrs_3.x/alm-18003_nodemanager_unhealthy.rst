:original_name: ALM-18003.html

.. _ALM-18003:

ALM-18003 NodeManager Unhealthy
===============================

Description
-----------

The system checks the number of unhealthy NodeManager nodes every 30 seconds, and compares the number with the threshold. The Unhealthy Nodes indicator has a default threshold. This alarm is generated when the value of the Unhealthy Nodes indicator exceeds the threshold.

To change the threshold, on FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn**. On the displayed page, choose **Configurations** > **All Configurations**, and change the value of **yarn.nodemanager.unhealthy.alarm.threshold**. You do not need to restart Yarn to make the change take effect.

The default threshold is 0. The alarm is generated when the number of unhealthy nodes exceeds the threshold, and is cleared when the number of unhealthy nodes is less than the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
18003    Major          Yes
======== ============== =====================

Parameters
----------

============== =======================================================
Name           Meaning
============== =======================================================
Source         Specifies the cluster for which the alarm is generated.
ServiceName    Specifies the service for which the alarm is generated.
RoleName       Specifies the role for which the alarm is generated.
HostName       Specifies the host for which the alarm is generated.
Unhealthy Host Specifies the list of hosts with unhealthy nodes.
============== =======================================================

Impact on the System
--------------------

-  The faulty NodeManager node cannot provide the Yarn service.
-  The number of containers decreases, so the cluster performance deteriorates.

Possible Causes
---------------

-  The hard disk space of the host where the NodeManager node resides is insufficient.
-  User **omm** does not have the permission to access a local directory on the NodeManager node.

Procedure
---------

**Check the hard disk space of the host.**

#. On the FusionInsight Manager, and choose **O&M** > **Alarm > Alarms**. Click |image1| before the alarm and obtain unhealthy nodes in **Additional Information**.

#. .. _alm-18003__li11711432184458:

   Choose **Cluster** > *Name of the desired cluster* **> Services > Yarn** > **Instance**, select the NodeManager instance corresponding to the host, choose **Instance Configurations** **> All Configurations** and view disks corresponding to **yarn.nodemanager.local-dirs** and **yarn.nodemanager.log-dirs**.

#. Choose **O&M > Alarm** **> Alarms**. In the alarm list, check whether the related disk has the alarm **ALM-12017 Insufficient Disk Capacity**.

   -  If yes, go to :ref:`4 <alm-18003__li32014413184458>`.
   -  If no, go to :ref:`5 <alm-18003__li64222725184458>`.

#. .. _alm-18003__li32014413184458:

   Rectify the disk fault based on **ALM-12017 Insufficient Disk Capacit** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-18003__li4571214184458>`.

#. .. _alm-18003__li64222725184458:

   Choose **Hosts** > *Name of the desired host .* On the **Dashboard** page, check the disk usage of the corresponding partition. Check whether the percentage of the used space of the mounted disk exceeds the value of **yarn.nodemanager.disk-health-checker.max-disk-utilization-per-disk-percentage**

   -  If yes, go to :ref:`6 <alm-18003__li54043174184458>`.
   -  If no, go to :ref:`7 <alm-18003__li4571214184458>`.

#. .. _alm-18003__li54043174184458:

   Reduce the disk usage to less than the value of **yarn.nodemanager.disk-health-checker.max-disk-utilization-per-disk-percentage**, wait for 10 to 20 minutes, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-18003__li4571214184458>`.

**Check the access permission of the local directory on each NodeManager node.**

7.  .. _alm-18003__li4571214184458:

    Obtain the NodeManager directory viewed in :ref:`2 <alm-18003__li11711432184458>`, log in to each NodeManager node as user **root**, and go to the obtained directory.

8.  Run the **ll** command to check whether the permission of the **localdir** and **containerlogs** folders is **755** and whether **User:Group** is **omm:ficommon**.

    -  If yes, no further action is required.
    -  If no, go to :ref:`9 <alm-18003__li55292474184458>`.

9.  .. _alm-18003__li55292474184458:

    Run the following command to set the permission to **755** and **User:Group** to **omm:ficommon**:

    **chmod 755** *<folder_name>*

    **chown omm:ficommon** *<folder_name>*

10. Wait for 10 to 20 minutes and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-18003__li64787675184458>`.

**Collect fault information.**

11. .. _alm-18003__li64787675184458:

    On the FusionInsight Manager in the active cluster, choose **O&M** > **Log > Download**.

12. Select **Yarn** in the required cluster from the **Service**.

13. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

14. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532927430.png
.. |image2| image:: /_static/images/en-us_image_0000001532607758.png
