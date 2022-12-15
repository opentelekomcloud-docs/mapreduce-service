:original_name: alm_25000.html

.. _alm_25000:

ALM-25000 LdapServer Service Unavailable
========================================

Description
-----------

The system checks the LdapServer service status every 30 seconds. This alarm is generated when the active and standby LdapServer services are abnormal.

This alarm is cleared when either of the LdapServer services restores.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
25000    Critical       Yes
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

When this alarm is generated, no operation can be performed for the KrbServer users and LdapServer users in the cluster. For example, users, user groups, or roles cannot be added, deleted, or modified, and user passwords cannot be changed on MRS Manager. The authentication for existing users in the cluster is not affected.

Possible Causes
---------------

-  The node where the LdapServer service locates is faulty.
-  The LdapServer process is abnormal.

Procedure
---------

#. Check whether the nodes where the two SlapdServer instances of the LdapServer service locate are faulty.

   a. Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. .. _alm_25000__en-us_topic_0191813909_aalm-25000_mmccppss_id:

      Choose **LdapServer** > **Instances**. Go to the LdapServer instance page to obtain the host name of the node where the two SlapdServer instances reside.

   c. On the **Alarms** page of MRS Manager, check whether the alarm ALM-12006 Node Fault is generated.

      -  If yes, go to :ref:`1.d <alm_25000__en-us_topic_0191813909_aalm-25000_mmccppss_step_4>`.
      -  If no, go to :ref:`2.a <alm_25000__en-us_topic_0191813909_li192616463126>`.

   d. .. _alm_25000__en-us_topic_0191813909_aalm-25000_mmccppss_step_4:

      Check whether the host name in the alarm information is the same as the actual host name in :ref:`1.b <alm_25000__en-us_topic_0191813909_aalm-25000_mmccppss_id>`.

      -  If yes, go to :ref:`1.e <alm_25000__en-us_topic_0191813909_aalm-25000_mmccppss_alarm53003>`.
      -  If no, go to :ref:`2.a <alm_25000__en-us_topic_0191813909_li192616463126>`.

   e. .. _alm_25000__en-us_topic_0191813909_aalm-25000_mmccppss_alarm53003:

      Rectify the fault by following steps provided in ALM-12006 Node Fault.

   f. In the alarm list, check whether the alarm ALM-25000 LdapServer Service Unavailable is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_25000__en-us_topic_0191813909_li572522141314>`.

#. Check whether the LdapServer process is in normal state.

   a. .. _alm_25000__en-us_topic_0191813909_li192616463126:

      Go to the cluster details page and choose **Alarms**.

   b. Check whether ALM-12007 Process Fault is generated.

      -  If yes, go to :ref:`2.c <alm_25000__en-us_topic_0191813909_aalm-25000_mmccppss_step_8>`.
      -  If no, go to :ref:`3 <alm_25000__en-us_topic_0191813909_li572522141314>`.

   c. .. _alm_25000__en-us_topic_0191813909_aalm-25000_mmccppss_step_8:

      Check whether the service name and host name in the alarm are consistent with the LdapServer service and host names.

      -  If yes, go to :ref:`2.d <alm_25000__en-us_topic_0191813909_alarm53004>`.
      -  If no, go to :ref:`3 <alm_25000__en-us_topic_0191813909_li572522141314>`.

   d. .. _alm_25000__en-us_topic_0191813909_alarm53004:

      Rectify the fault by following steps provided in ALM-12007 Process Fault.

   e. In the alarm list, check whether the alarm ALM-25000 LdapServer Service Unavailable is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_25000__en-us_topic_0191813909_li572522141314>`.

#. .. _alm_25000__en-us_topic_0191813909_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
