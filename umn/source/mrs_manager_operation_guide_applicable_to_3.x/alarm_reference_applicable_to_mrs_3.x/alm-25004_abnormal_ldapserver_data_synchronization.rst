:original_name: ALM-25004.html

.. _ALM-25004:

ALM-25004 Abnormal LdapServer Data Synchronization
==================================================

Description
-----------

The system checks the LdapServer data every 30 seconds. This alarm is generated when the data on the active and standby LdapServers of Manager is inconsistent for 12 consecutive times. This alarm is cleared when the data on the active and standby LdapServers is consistent.

The system checks the LdapServer data every 30 seconds. This alarm is generated when the LdapServer data in the cluster is inconsistent with that on Manager for 12 consecutive times. This alarm is cleared when the data is consistent.

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
Name        Meaning
=========== =======================================================
Source      Specifies the cluster for which the alarm is generated.
ServiceName Specifies the service for which the alarm is generated.
RoleName    Specifies the role for which the alarm is generated.
HostName    Specifies the host for which the alarm is generated.
=========== =======================================================

Impact on the System
--------------------

LdapServer data inconsistency occurs because the LdapServer data in Manager is damaged or the LdapServer data in the cluster is damaged. The LdapServer process with damaged data cannot provide services externally, and the authentication functions of Manager and the cluster are affected.

Possible Causes
---------------

-  The network of the node where the LdapServer process locates is faulty.
-  The LdapServer process is abnormal.
-  The OS restart damages data on LdapServer.

Procedure
---------

**Check whether the network where the LdapServer nodes reside is faulty.**

#. On the MRS Manager portal, choose **O&M > Alarm > Alarms**. Record the IP address of HostName in the alarm locating information as IP1 (if multiple alarms exist, record the IP addresses as IP1, IP2, and IP3 respectively).

#. Contact O&M personnel and log in to the nodes corresponding to IP 1. Run the ping command to check whether the IP address of the management plane of the active OMS node can be pinged.

   -  If yes, go to :ref:`4 <alm-25004__li16739739952>`.
   -  If no, go to :ref:`3 <alm-25004__li8942461952>`.

#. .. _alm-25004__li8942461952:

   Contact the network administrator to recover the network and check whether **Abnormal LdapServer Data Synchronization** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`4 <alm-25004__li16739739952>`.

**Check whether the LdapServer processes are normal.**

4. .. _alm-25004__li16739739952:

   On the **Alarm** page of MRS Manager, check whether the **OLdap Resource Abnormal** exists.

   -  If yes, go to :ref:`5 <alm-25004__li13741581952>`.
   -  If no, go to :ref:`7 <alm-25004__li40748590952>`.

5. .. _alm-25004__li13741581952:

   Clear the alarm by following the steps provided in "ALM-12004 OLdap Resource Abnormal".

6. Check whether **Abnormal LdapServer Data Synchronization** is cleared in the alarm list.

   -  If yes, no further action is required.
   -  If no, go to :ref:`7 <alm-25004__li40748590952>`.

7. .. _alm-25004__li40748590952:

   On the **Alarm** page of MRS Manager, check whether **Process Faul**\ t is generated for the LdapServer service.

   -  If yes, go to :ref:`8 <alm-25004__li12301476952>`.
   -  If no, go to :ref:`10 <alm-25004__li36315373952>`.

8. .. _alm-25004__li12301476952:

   Handle the alarm according to "ALM-12007 Process Fault".

9. Check whether **Abnormal LdapServer Data Synchronization** is cleared.

   -  If yes, no further action is required.
   -  If no, go to :ref:`10 <alm-25004__li36315373952>`.

**Check whether the LdapServer processes are normal.**

10. .. _alm-25004__li36315373952:

    On MRS Manager, choose **O&M** > **Alarm** > **Alarms**. Record the IP address of HostName in the alarm locating information as "IP1" (if multiple alarms exist, record the IP addresses as "IP1", "IP2", and "IP3" respectively). Choose **Cluster** > *Name of the desired cluster* > **Services** > **LdapServer** > **Configurations**. Record the port number of LdapServer as "PORT". (If the IP address in the alarm locating information is the IP address of the standby management node, choose **System** > **OMS** > **oldap** > **Modify Configuration** and record the listening port number of LdapServer.)

11. Log in to the nodes corresponding to IP1 as user **omm**.

12. Run the following command to check whether errors are displayed in the queried information.

    **ldapsearch -H ldaps://**\ *IP1*:*PORT* **-LLL -x -D cn=root,dc=hadoop,dc=com -W -b ou=Peoples,dc=hadoop,dc=com**

    After running the command, enter the **LDAP** administrator password. Contact the system administrator to obtain the password.

    -  If yes, go to :ref:`13 <alm-25004__li5200119952>`.
    -  If no, go to :ref:`15 <alm-25004__li40582301952>`.

13. .. _alm-25004__li5200119952:

    Recover the LdapServer and OMS nodes using data backed up before the alarm is generated.

    .. note::

       Use the OMS data and LdapServer data backed up at the same point in time to recover the data. Otherwise, the service and operation may fail. To recover data when services run properly, you are advised to manually back up the latest management data and then recover the data. Otherwise, Manager data produced between the backup point in time and the recovery point in time will be lost.

14. Check whether alarm **Abnormal LdapServer Data Synchronization** is cleared.

    -  If yes, no further action is required.
    -  If no, go to :ref:`15 <alm-25004__li40582301952>`.

**Collect fault information.**

15. .. _alm-25004__li40582301952:

    On the MRS Manager portal, choose **O&M** > **Log > Download**.

16. Select **LdapServer** in the required cluster and **OmsLdapServer** from the **Service**.

17. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

18. Contact the O&M personnel and send the collected logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532448478.png
