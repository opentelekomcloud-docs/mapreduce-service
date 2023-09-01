:original_name: ALM-19021.html

.. _ALM-19021:

ALM-19021 Handler Usage of RegionServer Exceeds the Threshold
=============================================================

Description
-----------

The system checks the RegionServer handler usage of each HBase service instance every 30 seconds. This alarm is generated when the handler usage of a RegionServer exceeds the threshold (90% for five consecutive times by default). This alarm is cleared if the handler usage is lower than or equal to the threshold.

.. note::

   This section applies to MRS 3.2.0 or later.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
19021    Major          Yes
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

RegionServers or HBase cannot provide services properly.

Possible Causes
---------------

-  The value of a handler is too small.
-  Hotspotting occurs.

Procedure
---------

**View alarm location information.**

#. Log in to FusionInsight Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms**, locate the row that contains the alarm whose **Alarm ID** is **19021**, and view the service instance and host name in **Location**.

**Check the handler configuration.**

2. Choose **Cluster** > **Services** > **HBase** and click the **Configurations** tab. In the upper right corner of the page, search for **hbase.regionserver.handler.count** and check whether its value is too small. The default value is **200**.

   -  If yes, go to :ref:`3 <alm-19021__li195843102017>`.
   -  If no, go to :ref:`5 <alm-19021__li5581133206>`.

3. .. _alm-19021__li195843102017:

   Change the value of this parameter to a greater value and save the configuration. Choose **Cluster** > **Services** > **HBase**, click the **Instance** tab, select the affected RegionServer instances, and choose **More** > **Instance Rolling Restart**. In the displayed dialog box, enter the username and password. In the **Instance Rolling Restart** dialog box, click **OK** and wait until the rolling restart is complete.

4. After the configuration takes effect, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-19021__li5581133206>`.

**Check whether cluster hotspotting occurs.**

5.  .. _alm-19021__li5581133206:

    On FusionInsight Manager, choose **Cluster** > **Services** > **HBase** and click **HMaster(Active)** following **HMaster WebUI** to go to the web UI of the HBase instance. In the **Region Servers** area of the **Home** page, click **Requests** and check whether the requests in the **Filtered Read Request Count** and **Write Request Count** columns are evenly distributed.

    |image1|

    -  If yes, go to :ref:`13 <alm-19021__li66014362013>`.
    -  If no, go to :ref:`6 <alm-19021__li6799182374314>`.

6.  .. _alm-19021__li6799182374314:

    Check whether regions are evenly distributed.

    On FusionInsight Manager, choose **Cluster** > **Services** > **HBase** and click **HMaster(Active)** following **HMaster WebUI** to go to the web UI of the HBase instance. In the **Region Servers** area of the **Home** page, click **Base Stats** and check whether the regions in the **Num.Regions** column are evenly distributed.

    |image2|

    -  If yes, go to :ref:`13 <alm-19021__li66014362013>`.
    -  If no, go to :ref:`7 <alm-19021__li25912310204>`.

7.  .. _alm-19021__li25912310204:

    Log in to the faulty RegionServer node as user **omm**.

8.  Run the following commands to go to the client installation directory and set the environment variable:

    **cd** *Client installation directory*

    **source bigdata_env**

    If the cluster uses the security mode, run the following command to perform security authentication:

    **kinit hbase**

    Enter the password as prompted (obtain the password from the MRS cluster administrator).

9.  Run the following commands to check whether the load balancing function is enabled. If the command output is **true**, the load balancing function is enabled.

    **hbase shell**

    **balancer_enabled**

    .. code-block::

       hbase:004:0> balancer_enabled
       true
       Took 0.0165 seconds
       => true

    -  If yes, go to :ref:`13 <alm-19021__li66014362013>`.
    -  If no, go to :ref:`10 <alm-19021__li1959839204>`.

10. .. _alm-19021__li1959839204:

    Run the following commands in HBase Shell to enable the load balancing function and check whether the function is enabled.

    **balance_switch true**

    **balancer_enabled**

    .. note::

       You are advised to enable and manually trigger the load balancing function during off-peak hours.

11. Run the following command to manually trigger' the load balancing function:

    **balancer**

12. After the load balancing is complete, log in to FusionInsight Manager and choose **O&M**. In the navigation pane on the left, choose **Alarm** > **Alarms** and check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`13 <alm-19021__li66014362013>`.

**Collect the fault information.**

13. .. _alm-19021__li66014362013:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

14. Expand the **Service** drop-down list, and select **HBase** for the target cluster.

15. Click |image3| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time respectively. Then, click **Download**.

16. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448374.png
.. |image2| image:: /_static/images/en-us_image_0000001583087517.png
.. |image3| image:: /_static/images/en-us_image_0000001532927534.png
