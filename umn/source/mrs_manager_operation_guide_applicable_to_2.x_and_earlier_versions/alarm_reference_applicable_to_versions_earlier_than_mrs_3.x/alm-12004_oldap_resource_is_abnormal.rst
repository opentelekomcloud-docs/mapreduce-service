:original_name: alm_12004.html

.. _alm_12004:

ALM-12004 OLdap Resource Is Abnormal
====================================

Description
-----------

This alarm is generated when the Ldap resource in Manager is abnormal.

This alarm is cleared when the Ldap resource in Manager recovers and the alarm handling is complete.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12004    Major          Yes
======== ============== ==========

Parameter
---------

=========== =======================================================
Parameter   Description
=========== =======================================================
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

The Manager authentication services are unavailable and cannot provide security authentication and user management functions for web upper-layer services. Users may be unable to log in to Manager.

Possible Causes
---------------

The LdapServer process in Manager is abnormal.

Procedure
---------

#. Check whether the LdapServer process in Manager is normal.

   a. Log in to the active management node.

   b. Run **ps -ef \| grep slapd** to check whether the LdapServer resource process in the **${BIGDATA_HOME}/om-0.0.1/** directory of the configuration file is running properly.

      You can determine that the resource is normal as follows:

      #. Run **sh ${BIGDATA_HOME}/om-0.0.1/sbin/status-oms.sh** and find that **ResHAStatus** of the OLdap process is **Normal**.
      #. Run **ps -ef \| grep slapd** and find that the slapd process occupies port 21750.

      -  If yes, go to :ref:`2 <alm_12004__en-us_topic_0191813880_li15577384153414>`.
      -  If no, go to :ref:`3 <alm_12004__en-us_topic_0191813935_li2924012813025>`.

#. .. _alm_12004__en-us_topic_0191813880_li15577384153414:

   Run **kill -2** *PID of the LdapServer process* and wait 20 seconds. The HA starts the OLdap process automatically. Check whether the status of the OLdap resource is normal.

   -  If yes, no further action is required.
   -  If no, go to :ref:`3 <alm_12004__en-us_topic_0191813935_li2924012813025>`.

#. .. _alm_12004__en-us_topic_0191813935_li2924012813025:

   Collect fault information.

   a. On MRS Manager, choose **System** > **Export Log**.
   b. Contact technical support engineers for help. For details, see `technical support <https://docs.otc.t-systems.com/en-us/public/learnmore.html>`__.

Reference
---------

None
