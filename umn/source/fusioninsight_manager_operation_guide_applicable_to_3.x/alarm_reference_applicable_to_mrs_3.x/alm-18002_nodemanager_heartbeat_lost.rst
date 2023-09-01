:original_name: ALM-18002.html

.. _ALM-18002:

ALM-18002 NodeManager Heartbeat Lost
====================================

Description
-----------

The system checks the number of lost NodeManager nodes every 30 seconds, and compares the number with the threshold. The Number of Lost Nodes indicator has a default threshold. The alarm is generated when the value of Number of Lost Nodes exceeds the threshold.

To change the threshold, on FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn**. On the displayed page, choose **Configurations** > **All Configurations**, and change the value of **yarn.nodemanager.lost.alarm.threshold**. You do not need to restart Yarn to make the change take effect.

The default threshold is 0. The alarm is generated when the number of lost nodes exceeds the threshold, and is cleared when the number of lost nodes is less than the threshold.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
18002    Major          Yes
======== ============== =====================

Parameters
----------

=========== =======================================================
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
Lost Host   Specifies the list of hosts with lost nodes.
=========== =======================================================

Impact on the System
--------------------

-  The lost NodeManager node cannot provide the Yarn service.
-  The number of containers decreases, so the cluster performance deteriorates.

Possible Causes
---------------

-  NodeManager is forcibly deleted without decommission.
-  All the NodeManager instances are stopped or the NodeManager process is faulty.
-  The host where the NodeManager node resides is faulty.
-  The network between the NodeManager and ResourceManager is disconnected or busy.

Procedure
---------

**Check the NodeManager status.**

#. .. _alm-18002__li45221725183746:

   On the FusionInsight Manager, and choose **O&M** > **Alarm > Alarms**. Click |image1| before the alarm and obtain lost nodes in **Additional Information**.

#. Check whether the lost nodes are hosts that have been manually deleted without decommission.

   -  If yes, go to :ref:`3 <alm-18002__li10848276183746>`.
   -  If no, go to :ref:`5 <alm-18002__li58395585183746>`.

#. .. _alm-18002__li10848276183746:

   After the setting, Choose **Cluster** > *Name of the desired cluster* > **Services** > **Yarn**. On the displayed page, choose **Configurations** > **All Configurations**. Search for **yarn.nodemanager.lost.alarm.threshold** and change its value to the number of hosts that are not out of service and proactively deleted. After the setting, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-18002__li30525620183746>`.

#. .. _alm-18002__li30525620183746:

   Manually clear the alarm. Note that decommission must be performed before deleting hosts.

#. .. _alm-18002__li58395585183746:

   On the FusionInsight Manager portal, choose **Cluster > Hosts**, and check whether the nodes obtained in :ref:`1 <alm-18002__li45221725183746>` are healthy.

   -  If yes, go to :ref:`7 <alm-18002__li26422237183746>`.
   -  If no, go to :ref:`6 <alm-18002__li3142189183746>`.

#. .. _alm-18002__li3142189183746:

   Rectify the node fault based on **ALM-12006 Node Fault** and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-18002__li26422237183746>`.

**Check the process status.**

7. .. _alm-18002__li26422237183746:

   On the FusionInsight Manager, choose **Cluster** > *Name of the desired cluster* **> Services** > **Yarn** > **Instance**, and check whether there are NodeManager instances whose status is not **Good**.

   -  If yes, go to :ref:`10 <alm-18002__li10762250183746>`.
   -  If no, go to :ref:`8 <alm-18002__li1508966183746>`.

8. .. _alm-18002__li1508966183746:

   Check whether the NodeManager instance is deleted.

   -  If yes, go to :ref:`9 <alm-18002__li42859132183746>`.
   -  If no, go to :ref:`11 <alm-18002__li13800982183746>`.

9. .. _alm-18002__li42859132183746:

   Restart the active and standby ResourceManager instances, and check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`13 <alm-18002__li34738119183746>`.

**Check the instance status.**

10. .. _alm-18002__li10762250183746:

    Select NodeManager instances which running state is not **Normal** and restart them. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`11 <alm-18002__li13800982183746>`.

**Check the network status.**

11. .. _alm-18002__li13800982183746:

    Log in to the management node, **ping** the IP address of the lost NodeManager node to check whether the network is disconnected or busy.

    -  If yes, go to :ref:`12 <alm-18002__li13119611183746>`.
    -  If no, go to :ref:`13 <alm-18002__li34738119183746>`.

12. .. _alm-18002__li13119611183746:

    Rectify the network, and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-18002__li34738119183746>`.

**Collect fault information.**

13. .. _alm-18002__li34738119183746:

    On the FusionInsight Manager in the active cluster, choose **O&M** > **Log > Download**.

14. Select **Yarn** in the required cluster from the **Service**.

15. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767534.png
.. |image2| image:: /_static/images/en-us_image_0000001532448310.png
