:original_name: alm_12010.html

.. _alm_12010:

ALM-12010 Manager Heartbeat Interruption Between the Active and Standby Nodes
=============================================================================

Description
-----------

This alarm is generated when the active Manager does not receive any heartbeat signal from the standby Manager within 7 seconds.

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

+-----------------------+---------------------------------------------------------+
| Parameter             | Description                                             |
+=======================+=========================================================+
| ServiceName           | Specifies the service for which the alarm is generated. |
+-----------------------+---------------------------------------------------------+
| RoleName              | Specifies the role for which the alarm is generated.    |
+-----------------------+---------------------------------------------------------+
| HostName              | Specifies the host for which the alarm is generated.    |
+-----------------------+---------------------------------------------------------+
| Local Manager HA Name | Specifies a local Manager HA.                           |
+-----------------------+---------------------------------------------------------+
| Peer Manager HA Name  | Specifies a peer Manager HA.                            |
+-----------------------+---------------------------------------------------------+

Impact on the System
--------------------

When the active Manager process is abnormal, an active/standby failover cannot be performed, and services are affected.

Possible Causes
---------------

The link between the active and standby Manager servers is abnormal.

Procedure
---------

#. Check whether the network between the active and standby Manager servers is normal.

   a. Go to the MRS cluster details page. In the alarm list on the alarm management tab page, click the row that contains the alarm. In the alarm details, view the address of the standby Manager server.

   b. Log in to the active management node.

   c. Run the following command to check whether the standby Manager is reachable:

      **ping** *heartbeat IP address of the standby Manager*

      -  If yes, go to :ref:`2 <alm_12010__li7265151273516>`.
      -  If no, go to :ref:`1.d <alm_12010__en-us_topic_0191813932_li233941717940>`.

   d. .. _alm_12010__en-us_topic_0191813932_li233941717940:

      Contact the O&M personnel to check whether the network is faulty.

      -  If yes, go to :ref:`1.e <alm_12010__en-us_topic_0191813932_li4279289717106>`.
      -  If no, go to :ref:`2 <alm_12010__li7265151273516>`.

   e. .. _alm_12010__en-us_topic_0191813932_li4279289717106:

      Rectify the network fault and check whether the alarm is cleared from the alarm list.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12010__li7265151273516>`.

#. .. _alm_12010__li7265151273516:

   Log in to all master nodes in the cluster and run the following commands to find all **sed**\ *xxx* files and delete them:

   **find /srv/BigData/ -name "sed*"**

   **find /opt -name "sed*"**

#. Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
