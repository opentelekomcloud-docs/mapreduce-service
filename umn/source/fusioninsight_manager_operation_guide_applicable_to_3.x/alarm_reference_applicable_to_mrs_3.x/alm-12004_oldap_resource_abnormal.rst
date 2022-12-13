:original_name: ALM-12004.html

.. _ALM-12004:

ALM-12004 OLdap Resource Abnormal
=================================

Description
-----------

The system checks LDAP resources every 60 seconds. This alarm is generated when the system detects that the LDAP resources in Manager are abnormal for six consecutive times.

This alarm is cleared when the Ldap resource in the Manager recovers and the alarm handling is complete.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
12004    Major          Yes
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

The Manager and component WebUI authentication services are unavailable and cannot provide security authentication and user management functions for web upper-layer services. Users may be unable to log in to the WebUIs of Manager and components.

Possible Causes
---------------

The LdapServer process in the Manager is abnormal.

Procedure
---------

**Check whether the LdapServer process in the Manager is normal.**

#. Log in the Manager node in the cluster as user **omm**.

   Log in to FusionInsight Manager using the floating IP address, and run the **sh ${BIGDATA_HOME}/om-server/om/sbin/status-oms.sh** command to check the information about the current Manager two-node cluster.

#. Run **ps -ef \| grep slapd** command to check whether the LdapServer resource process in the **${BIGDATA_HOME}/om-server/om/** in the process configuration file is running properly.

   .. note::

      You can determine that the resource is normal by checking the following information:

      a. After the **sh ${BIGDATA_HOME}/om-server/om/sbin/status-oms.sh** command runs, **ResHAStatus** of the OLdap is **Normal**.
      b. After the **ps -ef \| grep slapd** command runs, the slapd process of port 21750 can be viewed.

         -  If yes, go to :ref:`3 <alm-12004__l6ef892f9c8f749aa9e6871e1a63797b1>`.
         -  If no, go to :ref:`4 <alm-12004__l4b1abbc809ee41c28ade2b2c4cfa6fde>`.

#. .. _alm-12004__l6ef892f9c8f749aa9e6871e1a63797b1:

   Run the **kill -2** *ldap pid* command to restart the LdapServer process and wait for 20 seconds. The HA starts the OLdap process automatically. Check whether the current OLdap resource is in normal state.

   -  If yes, the operation is complete.
   -  If no, go to :ref:`4 <alm-12004__l4b1abbc809ee41c28ade2b2c4cfa6fde>`.

**Collect fault information.**

4. .. _alm-12004__l4b1abbc809ee41c28ade2b2c4cfa6fde:

   On the FusionInsight Manager home page, choose **O&M** > **Log > Download**.

5. Select **OmsLdapServer** and **OmmServer** from the **Service** and click **OK**.

6. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

7. Contact the O&M personnel and send the collected log information.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0269383809.png
