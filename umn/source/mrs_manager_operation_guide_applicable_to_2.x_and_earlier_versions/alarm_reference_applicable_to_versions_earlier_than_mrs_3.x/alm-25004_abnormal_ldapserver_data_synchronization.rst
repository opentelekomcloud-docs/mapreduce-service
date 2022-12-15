:original_name: alm_25004.html

.. _alm_25004:

ALM-25004 Abnormal LdapServer Data Synchronization
==================================================

Description
-----------

This alarm is generated when LdapServer data on Manager is inconsistent. This alarm is cleared when the data becomes consistent.

This alarm is generated when LdapServer data in the cluster is inconsistent with LdapServer data on Manager. This alarm is cleared when the data becomes consistent.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
25004    Critical       Yes
======== ============== ==========

Parameters
----------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

LdapServer data inconsistency occurs because LdapServer data on Manager or in the cluster is damaged. The LdapServer process with damaged data cannot provide services externally, and the authentication functions of Manager and the cluster are affected.

Possible Causes
---------------

-  The network of the node where the LdapServer process locates is faulty.
-  The LdapServer process is abnormal.
-  The OS restart damages data on LdapServer.

Procedure
---------

#. Check whether the network where the LdapServer nodes reside is faulty.

   a. Go to the cluster details page and choose **Alarms**.

   b. Record the IP address of **HostName** in **Location** of the alarm as **IP1** (if multiple alarms exist, record the IP addresses as **IP1**, **IP2**, and **IP3** respectively).

   c. Contact O&M personnel and use PuTTY to log in to the node corresponding to **IP1**. Run the **ping** command on the node to check whether the IP address of the management plane of the active OMS node can be pinged.

      -  If yes, go to :ref:`1.d <alm_25004__en-us_topic_0191813874_aalm-25004_mmccppss_step3>`.
      -  If no, go to :ref:`2.a <alm_25004__en-us_topic_0191813874_li4768141014141>`.

   d. .. _alm_25004__en-us_topic_0191813874_aalm-25004_mmccppss_step3:

      Contact O&M personnel to recover the network and check whether the alarm **ALM-25004 Abnormal LdapServer Data Synchronization** is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.a <alm_25004__en-us_topic_0191813874_li4768141014141>`.

#. Check whether the LdapServer process is in normal state.

   a. .. _alm_25004__en-us_topic_0191813874_li4768141014141:

      Go to the cluster details page and choose **Alarms**.

   b. Check whether ALM-12004 OLdap Resource Is Abnormal is generated for LdapServer.

      -  If yes, go to :ref:`2.c <alm_25004__en-us_topic_0191813874_aalm-25004_mmccppss_step5>`.
      -  If no, go to :ref:`2.e <alm_25004__en-us_topic_0191813874_aalm-25004_mmccppss_step7>`.

   c. .. _alm_25004__en-us_topic_0191813874_aalm-25004_mmccppss_step5:

      Rectify the fault by following steps provided in **ALM-12004 OLdap Resource Is Abnormal**.

   d. Check whether the alarm ALM-25004 Abnormal LdapServer Data Synchronization is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`2.e <alm_25004__en-us_topic_0191813874_aalm-25004_mmccppss_step7>`.

   e. .. _alm_25004__en-us_topic_0191813874_aalm-25004_mmccppss_step7:

      On the **Alarms** page of MRS Manager, check whether the alarm ALM-12007 Process Fault of LdapServer is generated.

      -  If yes, go to :ref:`2.f <alm_25004__en-us_topic_0191813874_step8>`.
      -  If no, go to :ref:`3.a <alm_25004__en-us_topic_0191813874_li1816316468144>`.

   f. .. _alm_25004__en-us_topic_0191813874_step8:

      Rectify the fault by following steps provided in ALM-12007 Process Fault.

   g. Check whether the alarm ALM-25004 Abnormal LdapServer Data Synchronization is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3.a <alm_25004__en-us_topic_0191813874_li1816316468144>`.

#. Check whether the OS restart damages data on LdapServer.

   a. .. _alm_25004__en-us_topic_0191813874_li1816316468144:

      Go to the cluster details page and choose **Alarms**.

   b. Record the IP address of **HostName** in **Location** of the alarm as **IP1** (if multiple alarms exist, record the IP addresses as **IP1**, **IP2**, and **IP3** respectively). Choose **Services** > **LdapServer** > **Service Configuration** and record the LdapServer port number as **PORT**. (If the IP address in the alarm location information is the IP address of the standby OMS node, the default port number is 21750.)

   c. Log in to node **IP1** as user **omm** and run the **ldapsearch -H ldaps://IP1:PORT -x -LLL -b dc=hadoop,dc=com** command (if the IP address is the IP address of the standby OMS node, run the **ldapsearch -H ldaps://IP1:PORT -x -LLL -b dc=hadoop,dc=com** command before running this command). Check whether error information is displayed in the command output.

      -  If yes, go to :ref:`3.d <alm_25004__en-us_topic_0191813874_aalm-25004_mmccppss_step12>`.
      -  If no, go to :ref:`4 <alm_25004__en-us_topic_0191813874_li572522141314>`.

   d. .. _alm_25004__en-us_topic_0191813874_aalm-25004_mmccppss_step12:

      Recover the LdapServer and OMS nodes using backup data before the alarm is generated. For details, see section "Recovering Manager Data" in the *Administrator Guide*.

      .. note::

         Use the OMS data and LdapServer data backed up at the same time to restore data. Otherwise, the service and operation may fail. To recover data when services run properly, you are advised to manually back up the latest management data and then recover the data. Otherwise, Manager data produced between the backup point in time and the recovery point in time will be lost.

   e. Check whether the alarm ALM-25004 Abnormal LdapServer Data Synchronization is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`4 <alm_25004__en-us_topic_0191813874_li572522141314>`.

#. .. _alm_25004__en-us_topic_0191813874_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
