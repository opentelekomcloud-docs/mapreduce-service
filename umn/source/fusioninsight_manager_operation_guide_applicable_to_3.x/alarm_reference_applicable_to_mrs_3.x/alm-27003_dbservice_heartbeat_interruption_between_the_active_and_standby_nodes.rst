:original_name: ALM-27003.html

.. _ALM-27003:

ALM-27003 DBService Heartbeat Interruption Between the Active and Standby Nodes
===============================================================================

Description
-----------

This alarm is generated when the active or standby DBService node does not receive heartbeat messages from the peer node for 7 seconds.

This alarm is cleared when the heartbeat recovers.

Attribute
---------

======== ============== =====================
Alarm ID Alarm Severity Automatically Cleared
======== ============== =====================
27003    Major          Yes
======== ============== =====================

Parameters
----------

+-------------------------+---------------------------------------------------------+
| Name                    | Meaning                                                 |
+=========================+=========================================================+
| Source                  | Specifies the cluster for which the alarm is generated. |
+-------------------------+---------------------------------------------------------+
| ServiceName             | Specifies the service for which the alarm is generated. |
+-------------------------+---------------------------------------------------------+
| RoleName                | Specifies the role for which the alarm is generated.    |
+-------------------------+---------------------------------------------------------+
| HostName                | Specifies the host for which the alarm is generated.    |
+-------------------------+---------------------------------------------------------+
| Local DBService HA Name | Specifies a local DBService HA.                         |
+-------------------------+---------------------------------------------------------+
| Peer DBService HA Name  | Specifies a peer DBService HA.                          |
+-------------------------+---------------------------------------------------------+

Impact on the System
--------------------

During the DBService heartbeat interruption, only one node can provide the service. If this node is faulty, no standby node is available for failover and the service is unavailable.

Possible Causes
---------------

The link between the active and standby DBService nodes is abnormal.

Procedure
---------

**Check whether the network between the active DBService server and the standby DBService server is normal.**

#. In the alarm list on FusionInsight Manager, click |image1| in the row where the alarm is located in the real-time alarm list and view the standby DBService server address.
#. Log in to the active DBService server as user **root**.

3. Run the **ping** *standby DBService heartbeat IP address* command to check whether the standby DBService server is reachable.

   -  If yes, go to :ref:`6 <alm-27003__li45543702195327>`.
   -  If no, go to :ref:`4 <alm-27003__li25387710195327>`.

4. .. _alm-27003__li25387710195327:

   Contact the network administrator to check whether the network is faulty.

   -  If yes, go to :ref:`5 <alm-27003__li34675550195327>`.
   -  If no, go to :ref:`6 <alm-27003__li45543702195327>`.

5. .. _alm-27003__li34675550195327:

   Rectify the network fault and check whether the alarm is cleared from the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-27003__li45543702195327>`.

**Collect fault information.**

6. .. _alm-27003__li45543702195327:

   On the FusionInsight Manager portal, choose **O&M** > **Log > Download**.

7. Select the following nodes in the required cluster from the **Service**:

   -  DBService
   -  Controller
   -  NodeAgent

8. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

9. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269417465.png
.. |image2| image:: /_static/images/en-us_image_0269417466.png
