:original_name: ALM-12010.html

.. _ALM-12010:

ALM-12010 Manager Heartbeat Interruption Between the Active and Standby Nodes
=============================================================================

Description
-----------

This alarm is generated when the active Mager does not receive the heartbeat signal from the standby Manager within 7 seconds.

This alarm is cleared when the active Manager receives heartbeat signals from the standby Manager.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12010    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+-------------------------------------------------------------------+
| Name        | Meaning                                                           |
+=============+===================================================================+
| Source      | Specifies the cluster or system for which the alarm is generated. |
+-------------+-------------------------------------------------------------------+
| ServiceName | Specifies the service for which the alarm is generated.           |
+-------------+-------------------------------------------------------------------+
| RoleName    | Specifies the role for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+
| HostName    | Specifies the host for which the alarm is generated.              |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

When the active Manager process is abnormal, an active/standby failover cannot be performed, and services are affected.

Possible Causes
---------------

-  The link between the active and standby Manager is abnormal.
-  The node name configuration is incorrect.
-  The port is disabled by the firewall.

Procedure
---------

**Check whether the network between the active and standby Manager server is normal.**

#. In the FusionInsight Manager portal, click **O&M > Alarm > Alarms**, click |image1| in the row containing the alarm and view the IP address of the standby Manager (Peer Manager) server in the alarm details.

#. Log in to the active Manager server as user **root**.

#. Run the **ping** *standby Manager heartbeat IP address* command to check whether the standby Manager server is reachable.

   -  If yes, go to :ref:`6 <alm-12010__li206521339172011>`.
   -  If no, go to :ref:`4 <alm-12010__li18651103915205>`.

#. .. _alm-12010__li18651103915205:

   Contact the network administrator to check whether the network is faulty.

   -  If yes, go to :ref:`5 <alm-12010__li166511739102017>`.
   -  If no, go to :ref:`6 <alm-12010__li206521339172011>`.

#. .. _alm-12010__li166511739102017:

   Rectify the network fault and check whether the alarm is cleared from the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12010__li206521339172011>`.

#. .. _alm-12010__li206521339172011:

   Run the following command to go to the software installation directory:

   **cd /opt**

#. Run the following command to find the configuration file directory of the active and standby nodes.

   **find -name hacom_local.xml**

#. Run the following command to go to the **workspace** directory:

   **cd${BIGDATA_HOME}/om-server/OMS/workspace0/ha/local/hacom/conf/**

#. Run the **vim** command to open the **hacom_local.xml** file. Check whether the local and peer nodes are correctly configured. The local node is configured as the active node, and the peer node is configured as the standby node.

   -  If yes, go to :ref:`12 <alm-12010__li56481639112012>`.
   -  If no, go to :ref:`10 <alm-12010__li18655163992011>`.

#. .. _alm-12010__li18655163992011:

   Modify the configuration of the active and standby nodes in the **hacom_local.xml** file and press **Esc** to return to the command mode. Run the **:wq** command to save the modification and exit.

#. Check whether the alarm is cleared automatically.

   -  If yes, no further action is required.
   -  If no, go to :ref:`12 <alm-12010__li56481639112012>`.

**Check whether the port is disabled by the firewall.**

12. .. _alm-12010__li56481639112012:

    Run the **lsof -i :20012** command to check whether the heartbeat ports of the active and standby nodes are enabled. If the command output is displayed, the ports are enabled. Otherwise, the ports are disabled by the firewall.

    -  If yes, go to :ref:`13 <alm-12010__li8648153982010>`.
    -  If no, go to :ref:`16 <alm-12010__li41244883171443>`.

13. .. _alm-12010__li8648153982010:

    Run the **iptables -P INPUT ACCEPT** command to avoid the server disconnection.

14. Run the following command to clear the firewall:

    **iptables -F**

15. Check whether the alarm is cleared from the alarm list.

    -  If yes, no further action is required.
    -  If no, go to :ref:`16 <alm-12010__li41244883171443>`.

**Collect fault information.**

16. .. _alm-12010__li41244883171443:

    On the FusionInsight Manager, choose **O&M** > **Log > Download**.

17. Select the following nodes from the **Service** and click **OK**:

    -  OmmServer
    -  Controller
    -  NodeAgent

18. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

19. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001583127401.png
.. |image2| image:: /_static/images/en-us_image_0000001532767502.png
