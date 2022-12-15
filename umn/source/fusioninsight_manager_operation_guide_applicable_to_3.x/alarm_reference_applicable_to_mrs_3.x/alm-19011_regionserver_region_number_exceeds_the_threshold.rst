:original_name: ALM-19011.html

.. _ALM-19011:

ALM-19011 RegionServer Region Number Exceeds the Threshold
==========================================================

Description
-----------

The system checks the number of regions on each RegionServer in each HBase service instance every 30 seconds. The region number is displayed on the HBase service monitoring page and RegionServer role monitoring page. This alarm is generated when the number of regions on a RegionServer exceeds the threshold (default value: 2000) for 20 consecutive times. The threshold can be changed by choosing **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **HBase**. This alarm is cleared when the number of regions is less than or equal to the threshold.

.. note::

   If the multi-instance function is enabled in the cluster and multiple HBase service instances are installed, you need to determine the HBase service instance where the alarm is generated based on the value of **ServiceName** in **Location**. For example, if the HBase1 service is unavailable, **ServiceName=HBase1** is displayed in **Location**, and the operation object in the procedure needs to be changed from HBase to HBase1.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
19011    Major          Yes
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

The data read/write performance of HBase is affected when the number of regions on a RegionServer exceeds the threshold.

Possible Causes
---------------

-  The RegionServer region distribution is unbalanced.
-  The HBase cluster scale is too small.

Procedure
---------

**View alarm location information.**

#. On the FusionInsight Manager home page, choose **O&M** > **Alarm** > **Alarms**, select this alarm, and view the service instance and host name in **Location**.

#. On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services**, click the HBase service instance for which the alarm is generated, and click **HMaster(Active)**. On the displayed WebUI of the HBase instance, check whether the region distribution on the RegionServer is balanced.

   .. note::

      By default, the **admin** user does not have the permissions to manage other components. If the page cannot be opened or the displayed content is incomplete when you access the native UI of a component due to insufficient permissions, you can manually create a user with the permissions to manage that component.

   -  If yes, go to :ref:`9 <alm-19011__li1035192916147>`.
   -  If no, go to :ref:`3 <alm-19011__li1094914149149>`.


   .. figure:: /_static/images/en-us_image_0276801805.png
      :alt: **Figure 1** WebUI of HBase instance

      **Figure 1** WebUI of HBase instance

**Enable load balancing.**

3. .. _alm-19011__li1094914149149:

   Log in to the node where the HBase client is located as user **root**. Go to the client installation directory, and set environment variables.

   **cd** *client installation directory*

   **source bigdata_env**

   If the cluster adopts the security mode, perform security authentication. Specifically, run the **kinit hbase** command and enter the password as prompted (obtain the password from the administrator).

4. Run the following commands to go to the HBase shell command window and check whether the load balancing function is enabled.

   **hbase shell**

   **balancer_enabled**

   -  If yes, go to :ref:`6 <alm-19011__li10954151421410>`.
   -  If no, go to :ref:`5 <alm-19011__li169541814111411>`.

5. .. _alm-19011__li169541814111411:

   On the HBase shell command window, run the following commands to enable the load balancing function and check whether the function is enabled.

   **balance_switch true**

   **balancer_enabled**

6. .. _alm-19011__li10954151421410:

   On the HBase shell command window, run the **balancer** command to manually trigger the load balancing function.

   .. note::

      You are advised to enable and manually trigger the load balancing function during off-peak hours.

7. On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase**, and click **HMaster(Active)**. On the displayed WebUI of the HBase instance, refresh the page and check whether the region distribution is balanced.

   -  If yes, go to :ref:`8 <alm-19011__li09541614181420>`.
   -  If no, go to :ref:`21 <alm-19011__li697624581415>`.

8. .. _alm-19011__li09541614181420:

   Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`9 <alm-19011__li1035192916147>`.

**Delete unwanted HBase tables.**

.. note::

   Exercise caution when deleting data to ensure data is deleted correctly.

9.  .. _alm-19011__li1035192916147:

    On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase**, and click **HMaster(Active)**. On the displayed WebUI of the HBase instance, view tables stored in the HBase service instance and record unwanted tables that can be deleted.

10. On the HBase shell command window, run the **disable** command and **drop** command to delete the table to decrease the number of regions.

    **disable '**\ *name of the table to be deleted'*

    **drop '**\ *name of the table to be deleted'*

11. On the HBase shell command window, run the following command to check whether the load balancing function is enabled.

    **balancer_enabled**

    -  If yes, go to :ref:`13 <alm-19011__li236102961418>`.
    -  If no, go to :ref:`12 <alm-19011__li33682961411>`.

12. .. _alm-19011__li33682961411:

    On the HBase shell command window, run the following commands to enable the load balancing function and confirm that the function is enabled.

    **balance_switch true**

    **balancer_enabled**

13. .. _alm-19011__li236102961418:

    On the HBase shell command window, run the **balancer** command to manually trigger the load balancing function.

14. On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase**, and click **HMaster(Active)**. On the displayed WebUI of the HBase instance, refresh the page and check whether the region distribution is balanced.

    -  If yes, go to :ref:`15 <alm-19011__li113716297149>`.
    -  If no, go to :ref:`21 <alm-19011__li697624581415>`.

15. .. _alm-19011__li113716297149:

    Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`16 <alm-19011__li3975164521415>`.

**Adjust the threshold.**

16. .. _alm-19011__li3975164521415:

    On the FusionInsight Manager home page, choose **O&M** > **Alarm** > **Thresholds** > *Name of the desired cluster* > **HBase** > **Regions(RegionServer)**, select the applied rule, and click **Modify** to check whether the threshold is proper.

    -  If it is excessively small, increase the threshold as required and go to :ref:`17 <alm-19011__li14975174511413>`.
    -  If it is proper, go to :ref:`18 <alm-19011__li4975174511141>`.

17. .. _alm-19011__li14975174511413:

    Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`18 <alm-19011__li4975174511141>`.

    **Perform system capacity expansion.**

18. .. _alm-19011__li4975174511141:

    Add nodes to the HBase cluster and add RegionServer instances to the nodes. Then enable and manually trigger the load balancing function.

19. On the FusionInsight Manager home page, choose **Cluster** > *Name of the desired cluster* > **Services**, click the HBase service instance for which the alarm is generated, and click **HMaster(Active)**. On the displayed WebUI of the HBase instance, refresh the page and check whether the region distribution is balanced.

    -  If yes, go to :ref:`20 <alm-19011__li119761945121413>`.
    -  If no, go to :ref:`21 <alm-19011__li697624581415>`.

20. .. _alm-19011__li119761945121413:

    Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`21 <alm-19011__li697624581415>`.

    **Collect fault information.**

21. .. _alm-19011__li697624581415:

    On the FusionInsight Manager home page of the active and standby clusters, choose **O&M**> **Log** > **Download**.

22. Select **HBase** in the required cluster from the **Service**.

23. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

24. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417427.png
