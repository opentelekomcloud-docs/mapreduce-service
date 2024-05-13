:original_name: ALM-19020.html

.. _ALM-19020:

ALM-19020 Number of HBase WAL Files to Be Synchronized Exceeds the Threshold
============================================================================

Description
-----------

The system checks the number of WAL files to be synchronized by the RegionServer of each HBase service instance every 30 seconds. This indicator can be viewed on the RegionServer role monitoring page. This alarm is generated when the number of WAL files to be synchronized on a RegionServer exceeds the threshold (exceeding 128 for 20 consecutive times by default). To change the threshold, choose **O&M** > **Alarm** > **Threshold Configuration** > *Name of the desired cluster* > **HBase** . This alarm is cleared when the number of WAL files to be synchronized is less than or equal to the threshold.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
19020    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------+---------------------------------------------------------+
| Name              | Meaning                                                 |
+===================+=========================================================+
| Source            | Specifies the cluster for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| ServiceName       | Specifies the service for which the alarm is generated. |
+-------------------+---------------------------------------------------------+
| RoleName          | Specifies the role for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| HostName          | Specifies the host for which the alarm is generated.    |
+-------------------+---------------------------------------------------------+
| Trigger Condition | Specifies the threshold for triggering the alarm.       |
+-------------------+---------------------------------------------------------+

Impact on the System
--------------------

If the number of WAL files to be synchronized by a RegionServer exceeds the threshold, the number of ZNodes used by HBase exceeds the threshold, affecting the HBase service status.

Possible Causes
---------------

-  The network is abnormal.
-  The RegionServer region distribution is unbalanced.
-  The HBase service scale of the standby cluster is too small.

Procedure
---------

View alarm location information.

#. Log in to MRS Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**. On the page that is displayed, locate the row containing the alarm whose **Alarm ID** is **19020**, and view the service instance and host name in **Location**.

Check the network connection between RegionServers on active and standby clusters.

2. Run the **ping** command to check whether the network connection between the faulty RegionServer node and the host where RegionServer of the standby cluster resides is normal.

   -  If yes, go to :ref:`5 <alm-19020__li11347192371020>`.
   -  If no, go to :ref:`3 <alm-19020__li1946854011118>`.

3. .. _alm-19020__li1946854011118:

   Contact the network administrator to restore the network.

4. After the network recovers, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-19020__li11347192371020>`.

Check the RegionServer region distribution in the active cluster.

5.  .. _alm-19020__li11347192371020:

    On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase**. Click **HMaster(Active)** to go to the web UI of the HBase instance and check whether regions are evenly distributed on the Region Server.

6.  .. _alm-19020__li277716529115:

    Log in to the faulty RegionServer node as user **omm**.

7.  Run the following commands to go to the client installation directory and set the environment variable:

    **cd** *Client installation directory*

    **source bigdata_env**

    If the cluster uses the security mode, perform security authentication. Run the **kinit hbase** command and enter the password as prompted (obtain the password from the MRS cluster administrator).

8.  Run the following commands to check whether the load balancing function is enabled.

    **hbase shell**

    **balancer_enabled**

    -  If yes, go to :ref:`10 <alm-19020__li127781952161113>`.
    -  If no, go to :ref:`9 <alm-19020__li8778145241118>`.

9.  .. _alm-19020__li8778145241118:

    Run the following commands in HBase Shell to enable the load balancing function and check whether the function is enabled.

    **balance_switch true**

    **balancer_enabled**

10. .. _alm-19020__li127781952161113:

    Run the **balancer** command to manually trigger the load balancing function.

    .. note::

       You are advised to enable and manually trigger the load balancing function during off-peak hours.

11. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-19020__li14354010126>`.

Check the HBase service scale of the standby cluster.

12. .. _alm-19020__li14354010126:

    Expand the HBase cluster, add a node, and add a RegionServer instance on the node. Then, perform :ref:`6 <alm-19020__li277716529115>` to :ref:`10 <alm-19020__li127781952161113>` to enable the load balancing function and manually trigger it.

13. On MRS Manager, choose **Cluster** > *Name of the desired cluster* > **Services** > **HBase**. Click **HMaster(Active)** to go to the web UI of the HBase instance, refresh the page, and check whether regions are evenly distributed.

    -  If yes, go to :ref:`14 <alm-19020__li435514181217>`.
    -  If no, go to :ref:`15 <alm-19020__li193977212510>`.

14. .. _alm-19020__li435514181217:

    Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`15 <alm-19020__li193977212510>`.

**Collect the fault information.**

15. .. _alm-19020__li193977212510:

    On MRS Manager of the standby cluster, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

16. Expand the **Service** drop-down list, and select **HBase** for the target cluster.

17. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

18. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583127517.png
