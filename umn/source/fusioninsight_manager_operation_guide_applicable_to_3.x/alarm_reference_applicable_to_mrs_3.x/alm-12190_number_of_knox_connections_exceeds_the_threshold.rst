:original_name: ALM-12190.html

.. _ALM-12190:

ALM-12190 Number of Knox Connections Exceeds the Threshold
==========================================================

Description
-----------

The system periodically checks the number of connections to all Knox topologies. This alarm is generated when the number of connections to a topology exceeds the threshold (90% by default). This alarm is automatically cleared when the number of connections to a topology falls below the threshold.

.. note::

   This alarm applies to clusters of MRS 3.1.0 or later.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12190    Major          Yes
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
| Topology    | Specifies the Knox topology for which the alarm is generated.     |
+-------------+-------------------------------------------------------------------+

Impact on the System
--------------------

The topology may reach the upper limit of connections and fail to forward requests, adversely affecting the MRS functions.

Possible Causes
---------------

Hue or Manager is too frequently used, but the default maximum number of Knox connections is small.

Procedure
---------

#. Log in to active and standby OMS nodes as user **root**, respectively.

#. Add the following configuration to the **gateway-site.xml** file on the active and standby OMS nodes to increase the number of thread pools:

   **vi /opt/knox/conf/gateway-site.xml**

   .. code-block::

      <property>
      <name>gateway.httpclient.maxConnections</name>
      <value>64</value>
      </property>

#. Log in to the active OMS node as user **omm** and run the following command to restart the Knox process:

   **sh /opt/knox/bin/restart-knox.sh**

#. After 5 minutes, check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`5 <alm-12190__li1980615424815>`.

#. .. _alm-12190__li1980615424815:

   Contact O&M personnel to rectify the fault.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None
