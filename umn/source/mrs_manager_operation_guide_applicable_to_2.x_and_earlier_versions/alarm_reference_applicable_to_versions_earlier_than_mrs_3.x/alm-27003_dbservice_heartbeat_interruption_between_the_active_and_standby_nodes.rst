:original_name: alm_27003.html

.. _alm_27003:

ALM-27003 DBService Heartbeat Interruption Between the Active and Standby Nodes
===============================================================================

Description
-----------

This alarm is generated when the active or standby DBService node does not receive heartbeat messages from the peer node.

This alarm is cleared when the heartbeat recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
27003    Major          Yes
======== ============== ==========

Parameters
----------

+-------------------------+---------------------------------------------------------+
| Parameter               | Description                                             |
+=========================+=========================================================+
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

#. Check whether the network between the active and standby DBService servers is in normal state.

   a. Go to the cluster details page and choose **Alarms**.

   b. In the alarm list, locate the row that contains the alarm and view the IP address of the standby DBService server in the alarm details.

   c. Log in to the active DBService server.

   d. Run the **ping** *heartbeat IP address of the standby DBService* command to check whether the standby DBService server is reachable.

      -  If yes, go to :ref:`2 <alm_27003__en-us_topic_0191813956_li572522141314>`.
      -  If no, go to :ref:`1.e <alm_27003__en-us_topic_0191813956_alm-27002_2_mmccppss_step2>`.

   e. .. _alm_27003__en-us_topic_0191813956_alm-27002_2_mmccppss_step2:

      Contact the network administrator to check whether the network is faulty.

      -  If yes, go to :ref:`1.f <alm_27003__en-us_topic_0191813956_alm-27002_2_mmccppss_s4>`.
      -  If no, go to :ref:`2 <alm_27003__en-us_topic_0191813956_li572522141314>`.

   f. .. _alm_27003__en-us_topic_0191813956_alm-27002_2_mmccppss_s4:

      Rectify the network fault and check whether the alarm is cleared from the alarm list.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_27003__en-us_topic_0191813956_li572522141314>`.

#. .. _alm_27003__en-us_topic_0191813956_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
