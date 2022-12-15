:original_name: alm_12011.html

.. _alm_12011:

ALM-12011 Data Synchronization Exception Between the Active and Standby Manager Nodes
=====================================================================================

Description
-----------

This alarm is generated when the standby Manager fails to synchronize files with the active Manager.

This alarm is cleared when the standby Manager synchronizes files with the active Manager.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12011    Critical       Yes
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

Because the configuration files on the standby Manager are not updated, some configurations will be lost after an active/standby switchover. Manager and some components may not run properly.

Possible Causes
---------------

The link between the active and standby Manager nodes is interrupted.

Procedure
---------

#. Check whether the network between the active and standby Manager servers is normal.

   a. Go to the MRS cluster details page. In the alarm list on the alarm management tab page, click the row that contains the alarm. In the alarm details, view the address of the standby Manager server.

   b. Log in to the active management node. Run the following command to check whether the standby Manager is reachable:

      **ping** *IP address of the standby Manager*

      -  If yes, go to :ref:`2 <alm_12011__en-us_topic_0191813887_li572522141314>`.
      -  If no, go to :ref:`1.c <alm_12011__en-us_topic_0191813887_li47267615172220>`.

   c. .. _alm_12011__en-us_topic_0191813887_li47267615172220:

      Contact the O&M personnel to check whether the network is faulty.

      -  If yes, go to :ref:`1.d <alm_12011__en-us_topic_0191813887_li37136917172238>`.
      -  If no, go to :ref:`2 <alm_12011__en-us_topic_0191813887_li572522141314>`.

   d. .. _alm_12011__en-us_topic_0191813887_li37136917172238:

      Rectify the network fault and check whether the alarm is cleared from the alarm list.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12011__en-us_topic_0191813887_li572522141314>`.

#. .. _alm_12011__en-us_topic_0191813887_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
