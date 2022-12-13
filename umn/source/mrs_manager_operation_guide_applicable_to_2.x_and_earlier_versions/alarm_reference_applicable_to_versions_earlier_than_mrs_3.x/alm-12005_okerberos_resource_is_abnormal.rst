:original_name: alm_12005.html

.. _alm_12005:

ALM-12005 OKerberos Resource Is Abnormal
========================================

Description
-----------

The alarm module monitors the status of the Kerberos resource in Manager. This alarm is generated when the Kerberos resource is abnormal.

This alarm is cleared when the alarm handling is complete and the Kerberos resource status recovers.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12005    Major          Yes
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

The authentication services are unavailable and cannot provide security authentication functions for web upper-layer services. Users may be unable to log in to MRS Manager.

Possible Causes
---------------

The OLdap resource on which OKerberos depends is abnormal.

Procedure
---------

#. Check whether the OLdap resource on which OKerberos depends is abnormal in Manager.

   a. Log in to the active management node.

   b. Run the following command to check whether the OLdap resource managed by HA is normal:

      **sh ${BIGDATA_HOME}/OMSV100R001C00x8664/workspace0/ha/module/hacom/script/status_ha.sh**

      The OLdap resource is normal when the OLdap resource is in the **Active_normal** state on the active node and in the **Standby_normal** state on the standby node.

      -  If yes, go to :ref:`3 <alm_12005__en-us_topic_0191813966_li572522141314>`.
      -  If no, go to :ref:`2 <alm_12005__en-us_topic_0191813966_li29509559161240>`.

#. .. _alm_12005__en-us_topic_0191813966_li29509559161240:

   Resolve the problem by following the instructions in :ref:`ALM-12004 OLdap Resource Is Abnormal <alm_12004>`. After the OLdap resource status recovers, check whether the OKerberos resource is normal.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm_12005__en-us_topic_0191813966_li572522141314>`.

#. .. _alm_12005__en-us_topic_0191813966_li572522141314:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
