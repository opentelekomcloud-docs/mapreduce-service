:original_name: alm_25500.html

.. _alm_25500:

ALM-25500 KrbServer Service Unavailable
=======================================

Description
-----------

The system checks the KrbServer service status every 30 seconds. This alarm is generated when the KrbServer service is abnormal.

This alarm is cleared when the KrbServer service is in normal state.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
25500    Critical       Yes
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

When this alarm is generated, no operation can be performed for the KrbServer component in the cluster. The authentication of KrbServer in other components will be affected. The health status of components that depend on KrbServer in the cluster is **Bad**.

Possible Causes
---------------

-  The node where the KrbServer service locates is faulty.
-  The OLdap service is unavailable.

Procedure
---------

#. Check whether the node where the KrbServer service locates is faulty.

   a. Go to the MRS cluster details page and click **Components**.

      .. note::

         For MRS 1.7.2 or earlier, log in to MRS Manager and click **Services**.

   b. .. _alm_25500__en-us_topic_0191813953_aalm-25500_mmccppss_id:

      Choose **KrbServer** > **Instances**. Go to the KrbServer instance page and view the host name of the node where the KrbServer service is deployed.

   c. On the **Alarms** page of MRS Manager, check whether the alarm ALM-12006 Node Fault is generated.

      -  If yes, go to :ref:`1.d <alm_25500__en-us_topic_0191813953_aalm-25500_mmccppss_step_4>`.
      -  If no, go to :ref:`2.a <alm_25500__en-us_topic_0191813953_li14191191521615>`.

   d. .. _alm_25500__en-us_topic_0191813953_aalm-25500_mmccppss_step_4:

      Check whether the host name in the alarm information is the same as the actual host name in :ref:`1.b <alm_25500__en-us_topic_0191813953_aalm-25500_mmccppss_id>`.

      -  If yes, go to :ref:`1.e <alm_25500__en-us_topic_0191813953_aalm-25500_mmccppss_alarm53003>`.
      -  If no, go to :ref:`2.a <alm_25500__en-us_topic_0191813953_li14191191521615>`.

   e. .. _alm_25500__en-us_topic_0191813953_aalm-25500_mmccppss_alarm53003:

      Rectify the fault by following steps provided in ALM-12006 Node Fault.

   f. In the alarm list, check whether the alarm ALM-25500 KrbServer Service Unavailable is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_25500__en-us_topic_0191813953_li572522141314>`.

#. Check whether the OLdap service is unavailable.

   a. .. _alm_25500__en-us_topic_0191813953_li14191191521615:

      Go to the cluster details page and choose **Alarms**.

   b. Check whether ALM-12004 OLdap Resource Is Abnormal is generated.

      -  If yes, go to :ref:`2.c <alm_25500__en-us_topic_0191813953_aalm-25500_mmccppss_step_8>`.
      -  If no, go to :ref:`3 <alm_25500__en-us_topic_0191813953_li572522141314>`.

   c. .. _alm_25500__en-us_topic_0191813953_aalm-25500_mmccppss_step_8:

      Rectify the fault by following steps provided in ALM-12004 OLdap Resource Is Abnormal.

   d. In the alarm list, check whether the alarm ALM-25500 KrbServer Service Unavailable is cleared.

      -  If yes, no further action is required.
      -  If no, go to :ref:`3 <alm_25500__en-us_topic_0191813953_li572522141314>`.

#. .. _alm_25500__en-us_topic_0191813953_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
