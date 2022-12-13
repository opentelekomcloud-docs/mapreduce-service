:original_name: ALM-12006.html

.. _ALM-12006:

ALM-12006 Node Fault
====================

Description
-----------

Controller checks the NodeAgent heartbeat every 30 seconds. If Controller does not receive heartbeat messages from a NodeAgent, it attempts to restart the NodeAgent process. This alarm is generated if the NodeAgent fails to be restarted for three consecutive times.

This alarm is cleared when Controller can properly receive the status report of the NodeAgent.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12006    Major          Yes
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

Services on the node are unavailable.

Possible Causes
---------------

The network is disconnected, the hardware is faulty, or the operating system runs slowly.

Procedure
---------

**Check whether the network is disconnected, whether the hardware is faulty, or whether the operating system runs commands slowly.**

#. On FusionInsight Manager, choose **O&M** > **Alarm** > **Alarms**. On the page that is displayed, click |image1| in the row containing the alarm, click the host name, and view the IP address of the host for which the alarm is generated.

#. Log in to the active management node as user **root**.

#. Run the **ping** *IP address of the faulty host* command to check whether the faulty node is reachable.

   -  If yes, go to :ref:`12 <alm-12006__li6096449165028>`.
   -  If no, go to :ref:`4 <alm-12006__li61437024165028>`.

#. .. _alm-12006__li61437024165028:

   Contact the network administrator to check whether the network is faulty.

   -  If yes, go to :ref:`5 <alm-12006__li23885090165028>`.
   -  If no, go to :ref:`6 <alm-12006__li9040006165028>`.

#. .. _alm-12006__li23885090165028:

   Rectify the network fault and check whether the alarm is cleared from the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`6 <alm-12006__li9040006165028>`.

#. .. _alm-12006__li9040006165028:

   Contact the hardware administrator to check whether the hardware (CPU or memory) of the node is faulty.

   -  If yes, go to :ref:`7 <alm-12006__li15590464165028>`.
   -  If no, go to :ref:`12 <alm-12006__li6096449165028>`.

#. .. _alm-12006__li15590464165028:

   Repair or replace faulty components and restart the node. Check whether the alarm is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`8 <alm-12006__li4828856593250>`.

#. .. _alm-12006__li4828856593250:

   If a large number of node faults are reported in the cluster, the floating IP addresses may be abnormal. As a result, Controller cannot detect the NodeAgent heartbeat.

   Log in to any management node and view the **/var/log/Bigdata/omm/oms/ha/scriptlog/floatip.log** log to check whether the logs generated one to two minutes before and after the faults occur are complete.

   For example, a complete log is in the following format:

   .. code-block::

      2017-12-09 04:10:51,000 INFO (floatip) Read from ${BIGDATA_HOME}/om-server_8.1.0.1/om/etc/om/routeSetConf.ini,value is : yes
      2017-12-09 04:10:51,000 INFO (floatip) check wsNetExport : eth0 is up.
      2017-12-09 04:10:51,000 INFO (floatip) check omNetExport : eth0 is up.
      2017-12-09 04:10:51,000 INFO (floatip) check wsInterface : eRth0:oms, wsFloatIp: XXX.XXX.XXX.XXX.
      2017-12-09 04:10:51,000 INFO (floatip) check omInterface : eth0:oms, omFloatIp: XXX.XXX.XXX.XXX.
      2017-12-09 04:10:51,000 INFO (floatip) check  wsFloatIp : XXX.XXX.XXX.XXX is reachable.
      2017-12-09 04:10:52,000 INFO (floatip) check  omFloatIp : XXX.XXX.XXX.XXX is reachable.

   -  If yes, go to :ref:`12 <alm-12006__li6096449165028>`.
   -  If no, go to :ref:`9 <alm-12006__li3216108493510>`.

#. .. _alm-12006__li3216108493510:

   Check whether the omNetExport log is printed after the wsNetExport is detected or whether the interval for printing two logs exceeds 10 seconds or longer.

   -  If yes, go to :ref:`10 <alm-12006__li1419227193519>`.
   -  If no, go to :ref:`12 <alm-12006__li6096449165028>`.

#. .. _alm-12006__li1419227193519:

   View the **/var/log/message** file of the OS to check whether sssd frequently restarts or nscd exception information is displayed when the fault occurs. For Red Hat, check sssd information. For SUSE, check nscd information.

   sssd restart example

   .. code-block::

      Feb  7 11:38:16 10-132-190-105 sssd[pam]: Shutting down
      Feb  7 11:38:16 10-132-190-105 sssd[nss]: Shutting down
      Feb  7 11:38:16 10-132-190-105 sssd[nss]: Shutting down
      Feb  7 11:38:16 10-132-190-105 sssd[be[default]]: Shutting down
      Feb  7 11:38:16 10-132-190-105 sssd: Starting up
      Feb  7 11:38:16 10-132-190-105 sssd[be[default]]: Starting up
      Feb  7 11:38:16 10-132-190-105 sssd[nss]: Starting up
      Feb  7 11:38:16 10-132-190-105 sssd[pam]: Starting up

   Example nscd exception information

   .. code-block::

      Feb 11 11:44:42 10-120-205-33 nscd: nss_ldap: failed to bind to LDAP server ldaps://10.120.205.55:21780: Can't contact LDAP server
      Feb 11 11:44:43 10-120-205-33 ntpq: nss_ldap: failed to bind to LDAP server ldaps://10.120.205.55:21780: Can't contact LDAP server
      Feb 11 11:44:44 10-120-205-33 ntpq: nss_ldap: failed to bind to LDAP server ldaps://10.120.205.92:21780: Can't contact LDAP server

   -  If yes, go to :ref:`11 <alm-12006__li5998962193529>`.
   -  If no, go to :ref:`12 <alm-12006__li6096449165028>`.

#. .. _alm-12006__li5998962193529:

   Check whether the LdapServer node is faulty, for example, the service IP address is unreachable or the network latency is too high. If the fault occurs periodically, locate and eliminate it and run the **top** command to check whether abnormal software exists.

**Collect the fault information.**

12. .. _alm-12006__li6096449165028:

    On FusionInsight Manager, choose **O&M**. In the navigation pane on the left, choose **Log** > **Download**.

13. Select the following nodes from **Services** and click **OK**.

    -  NodeAgent
    -  Controller
    -  OS

14. Click |image2| in the upper right corner, and set **Start Date** and **End Date** for log collection to 10 minutes ahead of and after the alarm generation time, respectively. Then, click **Download**.

15. Contact O&M personnel and provide the collected logs.

Alarm Clearing
--------------

This alarm is automatically cleared after the fault is rectified.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0263895827.png
.. |image2| image:: /_static/images/en-us_image_0263895607.png
