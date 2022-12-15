:original_name: admin_guide_000059.html

.. _admin_guide_000059:

Isolating a Host
================

Scenario
--------

If a host is abnormal or faulty and cannot provide services or affects the cluster performance, you can remove the host from the available node in the cluster temporarily so that the client can access other available nodes.

.. note::

   Only non-management nodes can be isolated.

Impact on the System
--------------------

-  After a host is isolated, all role instances on the host will be stopped, and you cannot start, stop, or configure the host and all instances on the host.
-  For some services, after a host is isolated, some instances on other nodes do not work, and the service configuration status may expire.
-  After a host is isolated, statistics about the monitoring status and indicator data of the host hardware and instances on the host cannot be collected or displayed.
-  Retain the default SSH port (22) of the target node. Otherwise, the task described in this section will fail.

Procedure
---------

#. Log in to FusionInsight Manager.

#. Click **Hosts**.

#. Select the check box of the host to be isolated.

#. Select **Isolate** from the **More** drop-down list.

   In the displayed dialog box, enter the password of the current login user and click **OK**.

#. In the displayed confirmation dialog box, select "I confirm to isolate the selected hosts and accept possible consequences of service faults." Click **OK**.

   Wait until the message "Operation succeeded" is displayed, and click **Finish**.

   The host is successfully isolated and **Running Status** is **Isolated**.

#. Log in to the isolated host as user **root** and run the **pkill -9 -u omm** command to stop the processes of user **omm** on the node. Then run the **ps -ef \| grep 'container' \| grep '${BIGDATA_HOME}' \| awk '{print $2}' \| xargs -I '{}' kill -9 '{}'** command to find and stop the container process.

#. Cancel the isolation status of the host before using the host if you have rectified the host exception or fault.

   On the **Hosts** page, select the isolated host and choose **More** > **Cancel Isolation**.

   .. note::

      After the isolation is canceled, all role instances on the host are not started by default. To start role instances on the host, select the target host on the Hosts page and choose **More** > **Start All Instances**.
