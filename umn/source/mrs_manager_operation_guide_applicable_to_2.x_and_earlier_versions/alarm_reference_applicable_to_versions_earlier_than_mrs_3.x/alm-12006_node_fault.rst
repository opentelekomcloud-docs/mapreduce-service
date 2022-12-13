:original_name: alm_12006.html

.. _alm_12006:

ALM-12006 Node Fault
====================

Description
-----------

Controller checks the NodeAgent status every 30 seconds. This alarm is generated when Controller fails to receive the status report of a NodeAgent for three consecutive times.

This alarm is cleared when Controller can properly receive the status report of the NodeAgent.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12006    Critical       Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

Services on the node are unavailable.

Possible Causes
---------------

The network is disconnected, or the hardware is faulty.

Procedure
---------

#. Check whether the network is disconnected or the hardware is faulty.

   a. Go to the MRS cluster details page. In the alarm list on the alarm management tab page, click the row that contains the alarm. In the alarm details, view the host address of the alarm.

   b. Log in to the active management node.

   c. Run the following command to check whether the faulty node is reachable:

      **ping** *IP address of the faulty host*

      #. If yes, go to :ref:`2 <alm_12006__en-us_topic_0191813934_li572522141314>`.
      #. If no, go to :ref:`1.d <alm_12006__en-us_topic_0191813934_li65085062161917>`.

   d. .. _alm_12006__en-us_topic_0191813934_li65085062161917:

      Contact the O&M personnel to check whether the network is faulty.

      -  If yes, go to :ref:`2 <alm_12006__en-us_topic_0191813934_li572522141314>`.
      -  If no, go to :ref:`1.f <alm_12006__en-us_topic_0191813934_li25618036162125>`.

   e. Rectify the network fault and check whether the alarm is cleared from the alarm list.

      -  If yes, no further action is required.
      -  If no, go to :ref:`1.f <alm_12006__en-us_topic_0191813934_li25618036162125>`.

   f. .. _alm_12006__en-us_topic_0191813934_li25618036162125:

      Contact the O&M personnel to check whether a hardware fault (for example, a CPU or memory fault) occurs on the node.

      -  If yes, go to :ref:`1.g <alm_12006__en-us_topic_0191813934_li8903046162132>`.
      -  If no, go to :ref:`2 <alm_12006__en-us_topic_0191813934_li572522141314>`.

   g. .. _alm_12006__en-us_topic_0191813934_li8903046162132:

      Repair the faulty components and restart the node. Check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2 <alm_12006__en-us_topic_0191813934_li572522141314>`.

#. .. _alm_12006__en-us_topic_0191813934_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
