:original_name: ALM-25006.html

.. _ALM-25006:

ALM-25006 Sssd Service Exception
================================

Description
-----------

The system checks the status of the sssd service every 60 seconds. This alarm is generated when the sssd process fails to be queried for four consecutive times (three minutes) or users in LdapServer cannot be obtained.

This alarm is cleared when the process is restored and users in LdapServer can be obtained.

Attribute
---------

======== ============== ==========
Alarm ID Alarm Severity Auto Clear
======== ============== ==========
25006    Major          Yes
======== ============== ==========

Parameters
----------

+-------------+------------------------------------------------------------------+
| Name        | Meaning                                                          |
+=============+==================================================================+
| Source      | Specifies the cluster for which the alarm is generated.          |
+-------------+------------------------------------------------------------------+
| ServiceName | Specifies the service name for which the alarm is generated.     |
+-------------+------------------------------------------------------------------+
| HostName    | Specifies the object (host ID) for which the alarm is generated. |
+-------------+------------------------------------------------------------------+

Impact on the System
--------------------

The alarmed node may not be able to synchronize data from LdapServer. The id command may fail to obtain the LDAP data, affecting upper-layer services.

Possible Causes
---------------

-  The sssd service is not started or is incorrectly started.
-  The network is faulty and cannot access the LDAP server.
-  NameService is abnormal.

-  Users cannot be queried because the OS executes commands too slowly.

Procedure
---------

**Check whether the sssd service is correctly started.**

#. On the MRS Manager portal, choose **O&M > Alarm > Alarms**. Find the IP address of **HostName** in **Location** of the alarm and record it as IP1 (if multiple alarms exist, record the IP addresses as IP1, IP2, and IP3 respectively).

#. .. _alm-25006__li872546684636:

   Contact the O&M personnel to access the node using IP1 as user root. Run the **ps -ef \| grep sssd** command and check whether the **/usr/sbin/sssd** process is started.

   -  If the process is started, go to :ref:`3 <alm-25006__li4389913484636>`.
   -  If the process is not started, go to :ref:`4 <alm-25006__li1838613984636>`.

#. .. _alm-25006__li4389913484636:

   Check whether the sssd process queried in :ref:`2 <alm-25006__li872546684636>` has three subprocesses.

   -  If yes, go to :ref:`5 <alm-25006__li9130384636>`.
   -  If no, go to :ref:`4 <alm-25006__li1838613984636>`.

#. .. _alm-25006__li1838613984636:

   Run the **service sssd restart** command as user **roo**\ t to restart the sssd service. Then run the **ps -ef \| grep sssd** command to check whether the sssd process is normal.

   In the normal state, the **/usr/sbin/sssd** process has three subprocesses: **/usr/libexec/sssd/sssd_be**, **/usr/libexec/sssd/sssd_nss**, and **/usr/libexec/sssd/sssd_pam**.

   -  If it exists, go to :ref:`9 <alm-25006__li4894866984636>`.
   -  If it does not exist, go to :ref:`13 <alm-25006__li4877321484636>`.

**Check whether the LDAP server can be accessed.**

5. .. _alm-25006__li9130384636:

   Log in to the alarmed node as user **root**. Run the **ping** command to check the network connectivity between this node and the LdapServer node.

   -  If the network is normal, go to :ref:`6 <alm-25006__li4687622084636>`.
   -  If the network is faulty, contact network administrators to troubleshoot the fault.

**Check whether NameService is normal.**

6. .. _alm-25006__li4687622084636:

   Log in to the alarmed node as user **root**. Run the **cat /etc/nsswitch.conf** command and check the **passwd** and **group** configurations of NameService.

   The correct parameter configurations are as follows: **passwd: compat ldap** and **group: compat ldap**.

   -  If the configurations are correct, go to :ref:`7 <alm-25006__li4799532284636>`.
   -  If the configurations are incorrect, go to :ref:`8 <alm-25006__li2317384684636>`.

7. .. _alm-25006__li4799532284636:

   Run the **/usr/sbin/sss_cache -G** and **/usr/sbin/sss_cache -U** commands as user **root**. Wait for 2 minutes and run the **id admin** and **id backup/manager** commands to check whether results can be queried.

   -  If results are queried, go to :ref:`9 <alm-25006__li4894866984636>`.
   -  If no result is queried, go to :ref:`13 <alm-25006__li4877321484636>`.

8. .. _alm-25006__li2317384684636:

   Run the **vi /etc/nsswitch.conf** command as user **root**. Correct the configurations in :ref:`6 <alm-25006__li4687622084636>` and save the file. Run the **service sssd restart** command to restart the sssd service. Wait for 2 minutes and run the **id admin** and **id backup/manager** commands to check whether results can be queried.

   -  If results are queried, go to :ref:`9 <alm-25006__li4894866984636>`.
   -  If no result is queried, go to :ref:`13 <alm-25006__li4877321484636>`.

9. .. _alm-25006__li4894866984636:

   Log in to the MRS Manager portal. Wait for 5 minutes and check whether the **sssd Service Exception** alarm is cleared.

   -  If the alarm is cleared, no further action is required.
   -  If the alarm persists, go to :ref:`10 <alm-25006__li44241319183338>`.

**Check whether frame freezing occurs when running a command in the operating system.**

10. .. _alm-25006__li44241319183338:

    Log in to the faulty node as user **root**, run the **id admin** command, and check whether the command execution takes a long time. If the command execution takes more than 3 seconds, the command execution is deemed to be slow.

    -  If yes, go to :ref:`11 <alm-25006__li10247506183338>`.
    -  If no, go to :ref:`13 <alm-25006__li4877321484636>`.

11. .. _alm-25006__li10247506183338:

    Run the **cat /var/log/messages** command to check whether the sssd frequently restarts or the error information **Can't contact LDAP server** exists.

    sssd restart example:

    .. code-block::

       Feb  7 11:38:16 10-132-190-105 sssd[pam]: Shutting down
       Feb  7 11:38:16 10-132-190-105 sssd[nss]: Shutting down
       Feb  7 11:38:16 10-132-190-105 sssd[nss]: Shutting down
       Feb  7 11:38:16 10-132-190-105 sssd[be[default]]: Shutting down
       Feb  7 11:38:16 10-132-190-105 sssd: Starting up
       Feb  7 11:38:16 10-132-190-105 sssd[be[default]]: Starting up
       Feb  7 11:38:16 10-132-190-105 sssd[nss]: Starting up
       Feb  7 11:38:16 10-132-190-105 sssd[pam]: Starting up

    -  If yes, go to :ref:`12 <alm-25006__li9709691183338>`.
    -  If no, go to :ref:`13 <alm-25006__li4877321484636>`.

12. .. _alm-25006__li9709691183338:

    Run the **vi $BIGDATA_HOME/tmp/random_ldap_ip_order** command to modify the number at the end. If the original number is an odd number, change it to an even number. If the number is an even number, change it to an odd number.

    Run the **vi /etc/sssd/sssd.conf** command to reverse the first two IP addresses of the **ldap_uri** configuration item, save the settings, and exit.

    Run the **ps -ef \| grep sssd** command to query the ID of the sssd process, kill it, and run the **/usr/sbin/sssd -D -f** command to restart the sssd service. Wait 5 minutes and run the **id admin** command again.

    Check whether the command execution is slow.

    -  If yes, go to :ref:`13 <alm-25006__li4877321484636>`.
    -  If no, log in to other faulty nodes and run :ref:`10 <alm-25006__li44241319183338>` to :ref:`12 <alm-25006__li9709691183338>`. Collect logs and check whether the first ldapserver node in the ldap_uri before modifying **/etc/sssd/sssd.conf** is faulty. For example, check whether the service IP address is unreachable, the network latency is too long, or other abnormal software is deployed.

**Collect fault information.**

13. .. _alm-25006__li4877321484636:

    On the MRS Manager portal, choose **O&M** > **Log > Download**.

14. Select **LdapClient** in the required cluster from the **Service**.

15. Click |image1| in the upper right corner, and set **Start Date** and **End Date** for log collection to 1 hour ahead of and after the alarm generation time, respectively. Then, click **Download**.

16. Contact the O&M personnel and send the collected fault logs.

Alarm Clearing
--------------

After the fault is rectified, the system automatically clears this alarm.

Related Information
-------------------

None

.. |image1| image:: /_static/images/en-us_image_0000001532767598.png
