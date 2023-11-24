:original_name: ALM-45640.html

.. _ALM-45640:

ALM-45640 FlinkServer Heartbeat Interruption Between the Active and Standby Nodes
=================================================================================

This section applies to MRS 3.2.0-LTS.2 or later.

Description
-----------

This alarm is generated when the FlinkServer active node or standby node does not receive heartbeat messages from the peer for 30 seconds (heartbeat interruption duration configured in keepalive).

This alarm is cleared when the heartbeat recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
45640    Minor          Yes
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

During the FlinkServer heartbeat interruption, only one node can provide the service. If this node is faulty, no standby node is available for failover and the service is unavailable.

Possible Causes
---------------

-  The active or standby FlinkServer instance is in the stopped state.
-  The NIC of the floating IP address of the HA system used by the FlinkServer node is incorrectly configured. FlinkServer fails to be started.
-  The link between the active and standby FlinkServer nodes is abnormal.

Procedure
---------

**Check the status of the active and standby FlinkServer instances.**

#. Log in to FusionInsight Manager, choose **Cluster** > **Services** > **Flink** > **Instance**, and check the state of FlinkServer is normal.

   -  If yes, go to :ref:`3 <alm-45640__li1192430217158>`.
   -  If no, go to :ref:`2 <alm-45640__li6097724617158>`.

#. .. _alm-45640__li6097724617158:

   Select the abnormal FlinkServer instance and start the instance. After the instance is started, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm-45640__li1192430217158>`.

**Check whether the link between the standby FlinkServer nodes is normal.**

3. .. _alm-45640__li1192430217158:

   Choose **Cluster** > **Services** > **Flink** > **Instance**, and check the two service IP addresses of FlinkServer.

4. Log in to the server where the abnormal FlinkServer instance locates as the **root** user.

5. Run the following command to check whether the server of the other FlinkServer instance is reachable:

   **ping** *IP address of the other FlinkServer instance*

   -  If yes, go to :ref:`8 <alm-45640__li1856073032510>`.
   -  If no, go to :ref:`6 <alm-45640__li6879155662418>`.

6. .. _alm-45640__li6879155662418:

   Ask the network administrator to handle the network exception.

7. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-45640__li1856073032510>`.

**Check whether the logs of the node where the abnormal FlinkServer instance locates contains error information.**

8.  .. _alm-45640__li1856073032510:

    Log in to the server where the abnormal FlinkServer instance locates as the **root** user.

9.  Open the log file in the default directory **/var/log/Bigdata/flink/flinkserver/prestart.log** and check whether there is error message **Float ip** *x.x.x.x* **is invalid**.

    -  If yes, go to :ref:`10 <alm-45640__li1885369317158>`.
    -  If no, go to :ref:`12 <alm-45640__li5131512717158>`.

10. .. _alm-45640__li1885369317158:

    On FusionInsight Manager, choose **Cluster** > **Services** > **Flink** > **Configurations** > **All Configurations** and search for **flink.ha.floatip**. Change the parameter value to the correct floating IP address, save the configuration, and restart the Flink service.

    .. note::

       Contact the network engineer to obtain the new floating IP address.

11. Check whether the alarm is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`12 <alm-45640__li5131512717158>`.

**Collect the fault information.**

12. .. _alm-45640__li5131512717158:

    On FusionInsight Manager, choose **O&M** > **Log** > **Download**.

13. Select the Flink service in the required cluster for **Service**.

14. Expand the **Hosts** drop-down list. In the **Select Host** dialog box that is displayed, select the hosts to which the role belongs, and click **OK**.

15. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583127285.png
