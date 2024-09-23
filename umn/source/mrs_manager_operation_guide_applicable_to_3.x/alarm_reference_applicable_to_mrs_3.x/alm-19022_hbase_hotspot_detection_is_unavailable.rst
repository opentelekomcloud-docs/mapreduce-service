:original_name: ALM-19022.html

.. _ALM-19022:

ALM-19022 HBase Hotspot Detection Is Unavailable
================================================

Alarm Description
-----------------

When the MetricController instance is installed for HBase, the alarm module checks the health status of the active HBase MetricController instance every 120 seconds. This alarm is generated when the active HBase MetricController instance does not exist or is unavailable and the hotspot detection function is unavailable.

This alarm is cleared when the active HBase MetricController instance recovers.

.. note::

   This alarm applies only to MRS 3.3.0 or later.

Alarm Attributes
----------------

======== ============== ============
Alarm ID Alarm Severity Auto Cleared
======== ============== ============
19022    Major          Yes
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

The HBase hotspot detection function is unavailable.

Possible Causes
---------------

-  The ZooKeeper service is abnormal.
-  The HBase service is abnormal.
-  In the current HBase service, the MetricController instance on the same node as the active HMaster instance is not started.
-  The network is abnormal.

Handling Procedure
------------------

**Check the ZooKeeper service status.**

#. In the service list on FusionInsight Manager, check whether **Running Status** of ZooKeeper is **Normal**.

   -  If yes, go to :ref:`5 <alm-19022__li18661164216271>`.
   -  If no, go to :ref:`2 <alm-19022__li1267193701920>`.

#. .. _alm-19022__li1267193701920:

   In the alarm list, check whether **ALM-13000 ZooKeeper Service Unavailable** exists.

   -  If yes, go to :ref:`3 <alm-19022__li667113714198>`.
   -  If no, go to :ref:`5 <alm-19022__li18661164216271>`.

#. .. _alm-19022__li667113714198:

   Rectify the fault by performing the operations provided for **ALM-13000 ZooKeeper Service Unavailable**.

#. Wait for several minutes and check whether the alarm **HBase Hotspot Detection Is Unavailable** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-19022__li18661164216271>`.

**Check the HBase service status.**

5. .. _alm-19022__li18661164216271:

   In the service list on FusionInsight Manager, check whether **Running Status** of HBase is **Normal**.

   -  If yes, go to :ref:`9 <alm-19022__li61381651152817>`.
   -  If no, go to :ref:`6 <alm-19022__li18662154292714>`.

6. .. _alm-19022__li18662154292714:

   In the alarm list, check whether the alarm ALM-19000 HBase Service Unavailable exists.

   -  If yes, go to :ref:`7 <alm-19022__li66625429278>`.
   -  If no, go to :ref:`9 <alm-19022__li61381651152817>`.

7. .. _alm-19022__li66625429278:

   Rectify the fault by following the steps provided for **ALM-19000 HBase Service Unavailable**.

8. Wait for several minutes and check whether the alarm **HBase Hotspot Detection Is Unavailable** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-19022__li61381651152817>`.

**Check whether the MetricController instance deployed on the same node as the active HMaster instance is started.**

9.  .. _alm-19022__li61381651152817:

    On FusionInsight Manager, choose **Cluster** > **Service** > **HBase**, and click **Instances** to check whether the **MetricController(Active)** instance exists.

    -  If yes, go to :ref:`12 <alm-19022__li182979395366>`.
    -  If no, go to :ref:`10 <alm-19022__li12138165182818>`.

10. .. _alm-19022__li12138165182818:

    Select the MetricController instance whose management IP address is the same as that of the active HMaster instance, and click **Start Instance**.

11. After the MetricController instance is restarted, check whether the alarm **HBase Hotspot Detection Is Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-19022__li182979395366>`.

**Check the network connectivity between the started MetricController instances and the active HMaster node.**

12. .. _alm-19022__li182979395366:

    Log in to the node where the active HMaser instance is deployed and run **ping** *IP address of the node where the standby MetricController instance is deployed* to check whether the network connection between the started MetricController instances and the host where the active HMaster instance is deployed is normal.

    -  If yes, go to :ref:`15 <alm-19022__li107641231103617>`.
    -  If no, go to :ref:`13 <alm-19022__li929715395365>`.

13. .. _alm-19022__li929715395365:

    Contact the network administrator to restore the network.

14. After the network recovers, check whether the alarm **HBase Hotspot Detection Is Unavailable** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`15 <alm-19022__li107641231103617>`.

**Collect fault information.**

15. .. _alm-19022__li107641231103617:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

16. Expand the **Service** drop-down list, and select **HBase** for the target cluster.

17. In the **Host** area, select the host where the HMaster instance is deployed.

18. Click the edit icon in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

19. Contact O&M personnel and provide the collected logs.

Alarm Clearance
---------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None.
