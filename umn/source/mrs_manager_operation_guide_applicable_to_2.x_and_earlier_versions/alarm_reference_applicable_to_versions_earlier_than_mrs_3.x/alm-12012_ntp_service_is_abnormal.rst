:original_name: alm_12012.html

.. _alm_12012:

ALM-12012 NTP Service Is Abnormal
=================================

Description
-----------

This alarm is generated when the NTP service on the current node fails to synchronize time with the NTP service on the active OMS node.

This alarm is cleared when the NTP service on the current node synchronizes time properly with the NTP service on the active OMS node.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12012    Major          Yes
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

The time on the node is inconsistent with that on other nodes in the cluster. Therefore, some MRS applications on the node may not run properly.

Possible Causes
---------------

-  The NTP service on the current node cannot start properly.
-  The current node fails to synchronize time with the NTP service on the active OMS node.
-  The key value authenticated by the NTP service on the current node is inconsistent with that on the active OMS node.
-  The time offset between the node and the NTP service on the active OMS node is large.

Procedure
---------

#. Check the NTP service on the current node.

   a. Check whether the ntpd process is running on the node using the following method. Log in to the node for which the alarm is generated and run the **sudo su - root** command to switch to user **root**. Then run the following command to check whether the command output contains the ntpd process:

      **ps -ef \| grep ntpd \| grep -v grep**

      -  If yes, go to :ref:`2.a <alm_12012__en-us_topic_0191813955_li64213271174322>`.
      -  If no, go to :ref:`1.b <alm_12012__en-us_topic_0191813955_li6445073917350>`.

   b. .. _alm_12012__en-us_topic_0191813955_li6445073917350:

      Run **service ntp start** to start the NTP service.

   c. Wait 10 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_12012__en-us_topic_0191813955_li64213271174322>`.

#. Check whether the current node can synchronize time properly with the NTP service on the active OMS node.

   a. .. _alm_12012__en-us_topic_0191813955_li64213271174322:

      Check whether the node can synchronize time with the NTP service on the active OMS node based on additional information of the alarm.

      If yes, go to :ref:`2.b <alm_12012__en-us_topic_0191813955_li14178567173544>`.

      If no, go to :ref:`3 <alm_12012__en-us_topic_0191813955_li65673991173316>`.

   b. .. _alm_12012__en-us_topic_0191813955_li14178567173544:

      Check whether the synchronization with the NTP service on the active OMS node is faulty.

      Log in to the node for which the alarm is generated, run the **sudo su - root** command to switch to user **root**, and run the **ntpq -np** command.

      If an asterisk (``*``) exists before the IP address of the NTP service on the active OMS node in the command output, the synchronization is in normal state. The command output is as follows:

      .. code-block::

         remote refid st t when poll reach delay offset jitter
         ==============================================================================
         *10.10.10.162 .LOCL. 1 u 1 16 377 0.270 -1.562 0.014

      If there is no asterisk (``*``) before the IP address of the NTP service on the active OMS node, as shown in the following command output, and the value of **refid** is **.INIT.**, the synchronization is abnormal.

      .. code-block::

         remote refid st t when poll reach delay offset jitter
         ==============================================================================
         10.10.10.162 .INIT. 1 u 1 16 377 0.270 -1.562 0.014

      -  If yes, go to :ref:`2.c <alm_12012__en-us_topic_0191813955_li25713785173557>`.
      -  If no, go to :ref:`3 <alm_12012__en-us_topic_0191813955_li65673991173316>`.

   c. .. _alm_12012__en-us_topic_0191813955_li25713785173557:

      Rectify the fault, wait 10 minutes, and then check whether the alarm is cleared.

      An NTP synchronization failure is usually related to the system firewall. If the firewall can be disabled, disable it and then check whether the fault is rectified. If the firewall cannot be disabled, check the firewall configuration policies and ensure that port **UDP 123** is enabled (you need to follow specific firewall configuration policies of each system).

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_12012__en-us_topic_0191813955_li65673991173316>`.

#. .. _alm_12012__en-us_topic_0191813955_li65673991173316:

   Check whether the key value authenticated by the NTP service on the current node is consistent with that on the active OMS node.

   Run **cat** **/etc/ntp.keys/etc/ntp/ntpkeys** to check whether the authentication code whose key value index is 1 is the same as the value of the NTP service on the active OMS node.

   -  If yes, go to :ref:`4.a <alm_12012__en-us_topic_0191813955_li50308011174636>`.
   -  If no, go to :ref:`5 <alm_12012__en-us_topic_0191813955_li572522141314>`.

#. Check whether the time offset between the node and the NTP service on the active OMS node is large.

   a. .. _alm_12012__en-us_topic_0191813955_li50308011174636:

      Check whether the time offset is large in additional information of the alarm.

      -  If yes, go to :ref:`4.b <alm_12012__en-us_topic_0191813955_li25272675173633>`.
      -  If no, go to :ref:`5 <alm_12012__en-us_topic_0191813955_li572522141314>`.

   b. .. _alm_12012__en-us_topic_0191813955_li25272675173633:

      On the **Hosts** page, select the host of the node, and choose **More** > **Stop All Roles** to stop all the services on the node.

      If the time on the alarm node is later than that on the NTP service of the active OMS node, adjust the time of the alarm node. After adjusting the time, choose **More** > **Start All Roles** to start the services on the node.

      If the time on the alarm node is earlier than that on the NTP service of the active OMS node, wait until the time offset is due and adjust the time of the alarm node. After adjusting the time, choose **More** > **Start All Roles** to start the services on the node.

      .. note::

         If you do not wait, data loss may occur.

   c. Wait 10 minutes and check whether the alarm is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`5 <alm_12012__en-us_topic_0191813955_li572522141314>`.

#. .. _alm_12012__en-us_topic_0191813955_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
